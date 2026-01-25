<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center - Full Auth + Orders</title>
<style>
body{margin:0;font-family:Arial;background:#0b0b0b;color:#fff}
header{padding:20px;text-align:center;background:linear-gradient(90deg,#ff003c,#1e90ff);box-shadow:0 0 15px #ff003c}
header h1{margin:0;font-size:28px}
header p{margin:5px;font-size:16px;color:#ccc}
.auth{padding:20px;text-align:center;background:#111;margin:20px auto;border-radius:10px;max-width:400px;box-shadow:0 0 15px #ff003c}
.auth input{width:90%;padding:10px;margin:5px 0;border-radius:6px;border:none}
.auth button{padding:10px;border:none;border-radius:6px;background:#ff003c;color:#fff;cursor:pointer;margin-top:10px;width:95%}
#logoutBtn{padding:10px;border:none;border-radius:6px;background:#1e90ff;color:#fff;cursor:pointer;margin:10px}
.features{padding:15px;background:#111;border-bottom:2px solid #ff003c;border-radius:0 0 10px 10px}
.features h3{margin-top:0;color:#ffcc00}
.features ul{list-style:disc;padding-left:20px;color:#ccc}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:15px;padding:20px}
.card{background:#111;padding:10px;border-radius:10px;box-shadow:0 0 15px #ff003c;transition:.3s;position:relative}
.card:hover{transform:scale(1.05)}
.card img{width:100%;height:180px;object-fit:cover;border-radius:8px}
.card h4{margin:5px 0;font-size:16px}
.card .cat{font-size:14px;color:#ccc}
.price{color:#00ffcc;font-weight:bold;margin:5px 0}
button.secondary{background:#1e90ff}
#cartBtn{position:fixed;bottom:20px;right:20px;padding:12px;border-radius:50%;background:#1e90ff;cursor:pointer;font-size:18px}
#cartBox{display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:#000c;z-index:99;overflow:auto}
#cart{background:#111;margin:40px auto;padding:20px;border-radius:12px;max-width:450px}
.cart-item{display:flex;justify-content:space-between;margin:6px 0;border-bottom:1px solid #333;padding-bottom:4px}
input,select{width:100%;padding:8px;margin:5px 0;border-radius:6px;border:none}
.social-icons{display:flex;gap:10px;margin-top:10px}
.social-icons a{color:#fff;text-decoration:none;font-size:20px}
footer{text-align:center;padding:15px;background:#111;color:#fff;font-size:14px}
</style>
</head>
<body>

<header>
<h1>Shopping Center</h1>
<p>Premium Online Store - Verified Products</p>
</header>

<div id="authDiv" class="auth">
<h3>Signup / Login</h3>
<input type="email" id="email" placeholder="Email">
<input type="password" id="password" placeholder="Password">
<button onclick="signup()">Sign Up</button>
<button onclick="login()">Login</button>
<p id="authMsg" style="color:#ff003c"></p>
</div>

<div id="userDiv" style="display:none; text-align:center;">
<h3>Welcome, <span id="userEmail"></span></h3>
<button id="logoutBtn" onclick="logout()">Logout</button>
</div>

<div class="features">
<h3>Why Shop With Us?</h3>
<ul>
<li>50+ Trending Products for Men, Women & Kids</li>
<li>Secure & Fast Payment Options</li>
<li>Easy Order via WhatsApp, Email, Instagram, Facebook</li>
<li>Exclusive Offers & Discounts</li>
<li>Free Delivery on Orders above PKR 5000</li>
</ul>
</div>

<div class="products" id="products"></div>

<button id="cartBtn" onclick="toggleCart()">🛒 Cart (<span id="cartCount">0</span>)</button>

<div id="cartBox">
<div id="cart">
<h3>Your Cart</h3>
<div id="cartItems"></div>
<h4>Total: <span id="total">0</span> PKR</h4>
<h3>Checkout</h3>

<input id="c_name" placeholder="Name">
<input id="c_phone" placeholder="WhatsApp Number">

<select id="payment"></select>

<p>
<b>Payment placeholders (edit yourself):</b><br>
EasyPaisa: 03XXXXXXXXX<br>
JazzCash: 03XXXXXXXXX<br>
Bank IBAN HERE
</p>

<input id="trx" placeholder="Transaction ID">

<div class="social-icons">
<a href="#" onclick="orderSocial('WhatsApp')">📱 WhatsApp</a>
<a href="#" onclick="orderSocial('Email')">✉️ Email</a>
<a href="#" onclick="orderSocial('Instagram')">📸 Instagram</a>
<a href="#" onclick="orderSocial('Facebook')">📘 Facebook</a>
</div>

<button onclick="placeOrder()">Place Order</button>
<button class="secondary" onclick="toggleCart()">Close</button>
</div>
</div>

<footer>Shopping Center © 2026 - All Rights Reserved</footer>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-app.js";
import { getDatabase, ref, push } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-database.js";
import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, onAuthStateChanged, sendEmailVerification, signOut } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-auth.js";

// Firebase config
const firebaseConfig = {
apiKey: "AIzaSyAL7_6DTdz14ySlLQ1jjuQC4WdO4mpRZKY",
authDomain: "shopping-center-9.firebaseapp.com",
projectId: "shopping-center-9",
storageBucket: "shopping-center-9.firebasestorage.app",
messagingSenderId: "33427127023",
appId: "1:33427127023:web:a478af6499f28f84d9391a"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
const db = getDatabase(app);
const auth = getAuth(app);

let products=[];
const categories=["Men","Women","Kids","Winter","Accessories","Electronics","Shoes"];
const types=["Shirt","T-Shirt","Jeans","Shoes","Watch","Bag","Jacket"];
for(let i=1;i<=50;i++){
products.push({
id:i,
name:`${categories[i%categories.length]} ${types[i%types.length]} ${i}`,
category:categories[i%categories.length],
type:types[i%types.length],
price:1000+i*50,
img:`https://source.unsplash.com/400x300/?${types[i%types.length]},${categories[i%categories.length]}`,
payment:["EasyPaisa","JazzCash","Bank Transfer"][i%3]
});
}

let cart=JSON.parse(localStorage.getItem("cart")||"[]");

function renderProducts(){
let p=document.getElementById("products");
p.innerHTML="";
products.forEach(prod=>{
p.innerHTML+=`
<div class="card">
<img src="${prod.img}">
<h4>${prod.name}</h4>
<div class="cat">${prod.category} - ${prod.type}</div>
<div class="price">PKR ${prod.price}</div>
<button onclick='addToCart(${JSON.stringify(prod)})'>Add to Cart</button>
</div>`;
});
updateCart();
}

function addToCart(prod){
cart.push(prod);
localStorage.setItem("cart",JSON.stringify(cart));
updateCart();
updatePaymentOptions();
}

function updateCart(){
document.getElementById("cartCount").innerText=cart.length;
let box=document.getElementById("cartItems"); box.innerHTML="";
let total=0;
cart.forEach(i=>{
total+=i.price;
box.innerHTML+=`<div class="cart-item">${i.name} - ${i.price} PKR</div>`;
});
document.getElementById("total").innerText=total;
}

function toggleCart(){
let c=document.getElementById("cartBox");
c.style.display=c.style.display=="block"?"none":"block";
updatePaymentOptions();
updateCart();
}

function updatePaymentOptions(){
let pay=document.getElementById("payment");
pay.innerHTML="";
let uniqueMethods=[...new Set(cart.map(c=>c.payment))];
uniqueMethods.forEach(m=>{
let opt=document.createElement("option");
opt.value=m; opt.innerText=m;
pay.appendChild(opt);
});
if(uniqueMethods.length==0){
let opt=document.createElement("option");
opt.value="EasyPaisa"; opt.innerText="EasyPaisa";
pay.appendChild(opt);
}
}

// Orders
function placeOrder(){
if(!auth.currentUser){alert("Login first!"); return;}
if(cart.length==0){alert("Cart empty!"); return;}
const orderData={
uid:auth.currentUser.uid,
email:auth.currentUser.email,
name:document.getElementById("c_name").value,
phone:document.getElementById("c_phone").value,
payment:document.getElementById("payment").value,
trx:document.getElementById("trx").value,
total:document.getElementById("total").innerText,
items:cart
};
push(ref(db,'orders'),orderData)
.then(()=>{alert("Order placed & saved!");cart=[];localStorage.setItem("cart",JSON.stringify(cart));toggleCart();});
}

// Social order buttons
function orderSocial(platform){
if(cart.length==0){alert("Cart empty!"); return;}
let msg=platform+" ORDER%0A";
cart.forEach(i=>msg+=`${i.name} - ${i.price} PKR - Payment: ${i.payment}%0A`);
msg+=`Total: ${document.getElementById("total").innerText} PKR%0A`;
msg+=`Name: ${c_name.value}%0APhone: ${c_phone.value}%0APayment Selected: ${payment.value}%0ATRX: ${trx.value}`;
let url="";
switch(platform){
case "WhatsApp": url="https://wa.me/92XXXXXXXXX?text="+msg; break;
case "Email": url="mailto:example@email.com?subject=Order&body="+msg; break;
case "Instagram": url="https://instagram.com/direct/inbox?text="+msg; break;
case "Facebook": url="https://www.facebook.com/messages/t/?message="+msg; break;
}
window.open(url,"_blank");
}

// Firebase Auth
function signup(){
const email=document.getElementById("email").value;
const pass=document.getElementById("password").value;
createUserWithEmailAndPassword(auth,email,pass)
.then(userCred=>{
sendEmailVerification(userCred.user)
.then(()=>{document.getElementById("authMsg").innerText="Verification email sent!"})
.catch(err=>{document.getElementById("authMsg").innerText=err.message});
})
.catch(err=>{document.getElementById("authMsg").innerText=err.message});
}

function login(){
const email=document.getElementById("email").value;
const pass=document.getElementById("password").value;
signInWithEmailAndPassword(auth,email,pass)
.then(userCred=>{
if(!userCred.user.emailVerified){alert("Verify your email first!"); return;}
document.getElementById("authDiv").style.display="none";
document.getElementById("userDiv").style.display="block";
document.getElementById("userEmail").innerText=userCred.user.email;
})
.catch(err=>{document.getElementById("authMsg").innerText=err.message});
}

function logout(){
signOut(auth).then(()=>{document.getElementById("authDiv").style.display="block";document.getElementById("userDiv").style.display="none";});
}

onAuthStateChanged(auth,user=>{
if(user && user.emailVerified){
document.getElementById("authDiv").style.display="none";
document.getElementById("userDiv").style.display="block";
document.getElementById("userEmail").innerText=user.email;
}else{
document.getElementById("authDiv").style.display="block";
document.getElementById("userDiv").style.display="none";
}
});

renderProducts();
</script>
</body>
</html>
