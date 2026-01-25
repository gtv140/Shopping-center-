<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center - Live Ready</title>
<style>
body{margin:0;font-family:Arial;background:#0b0b0b;color:#fff}
header{padding:20px;text-align:center;background:linear-gradient(90deg,#ff003c,#1e90ff);box-shadow:0 0 15px #ff003c}
header h1{margin:0;font-size:28px}
header p{margin:5px;font-size:16px;color:#ccc}
.auth, .admin, .products-section, #cartBox{padding:20px;margin:20px auto;border-radius:10px;max-width:450px;background:#111;box-shadow:0 0 15px #ff003c}
.auth input, .admin input, .products-section input, .products-section select{width:95%;padding:10px;margin:5px 0;border-radius:6px;border:none}
.auth button, .admin button, .products-section button{padding:10px;border:none;border-radius:6px;background:#ff003c;color:#fff;cursor:pointer;margin-top:10px;width:95%}
button.secondary{background:#1e90ff}
#logoutBtn{padding:10px;border:none;border-radius:6px;background:#1e90ff;color:#fff;cursor:pointer;margin:10px}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:15px;padding:20px}
.card{background:#111;padding:10px;border-radius:10px;box-shadow:0 0 15px #ff003c;transition:.3s;position:relative}
.card:hover{transform:scale(1.05)}
.card img{width:100%;height:180px;object-fit:cover;border-radius:8px}
.card h4{margin:5px 0;font-size:16px}
.card .cat{font-size:14px;color:#ccc}
.price{color:#00ffcc;font-weight:bold;margin:5px 0}
#cartBtn{position:fixed;bottom:20px;right:20px;padding:12px;border-radius:50%;background:#1e90ff;cursor:pointer;font-size:18px}
#cartBox{display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:#000c;z-index:99;overflow:auto}
#cart{background:#111;margin:40px auto;padding:20px;border-radius:12px;max-width:450px}
.cart-item{display:flex;justify-content:space-between;margin:6px 0;border-bottom:1px solid #333;padding-bottom:4px}
.social-icons{display:flex;gap:10px;margin-top:10px}
.social-icons a{color:#fff;text-decoration:none;font-size:20px}
footer{text-align:center;padding:15px;background:#111;color:#fff;font-size:14px}
</style>
</head>
<body>

<header>
<h1>Shopping Center</h1>
<p>Premium Online Store - Admin & User</p>
</header>

<!-- AUTH -->
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

<!-- ADMIN LOGIN -->
<div id="adminDiv" class="admin" style="display:none;">
<h3>Admin Login</h3>
<input type="password" id="adminPass" placeholder="Admin Password">
<button onclick="adminLogin()">Login</button>
<p id="adminMsg" style="color:#ff003c"></p>
</div>

<!-- ADMIN DASHBOARD -->
<div id="adminPanel" class="admin" style="display:none;">
<h3>Admin Panel</h3>
<h4>Orders</h4>
<div id="adminOrders"></div>
<h4>Add Product</h4>
<input id="pName" placeholder="Product Name">
<input id="pCategory" placeholder="Category">
<input id="pType" placeholder="Type">
<input id="pPrice" placeholder="Price">
<input id="pImg" placeholder="Image URL">
<select id="pPayment">
<option>EasyPaisa</option>
<option>JazzCash</option>
<option>Bank Transfer</option>
</select>
<button onclick="addProduct()">Add Product</button>
<button class="secondary" onclick="logoutAdmin()">Logout Admin</button>
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
import { getDatabase, ref, push, onValue } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-database.js";
import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, onAuthStateChanged, sendEmailVerification, signOut } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-auth.js";

// Firebase Config
const firebaseConfig = {
apiKey: "AIzaSyAL7_6DTdz14ySlLQ1jjuQC4WdO4mpRZKY",
authDomain: "shopping-center-9.firebaseapp.com",
projectId: "shopping-center-9",
storageBucket: "shopping-center-9.firebasestorage.app",
messagingSenderId: "33427127023",
appId: "1:33427127023:web:a478af6499f28f84d9391a"
};
const app = initializeApp(firebaseConfig);
const db = getDatabase(app);
const auth = getAuth(app);

// Admin Password
const ADMIN_PASS = "admin123";

// Products with curated images
let products=[
{id:1,name:"Men Shirt 1",category:"Men",type:"Shirt",price:1200,img:"https://images.unsplash.com/photo-1618354695482-8b8f1672f449?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8bWVucyUyMHNoaXJ0fGVufDB8fDB8&ixlib=rb-4.0.3&w=400",payment:"EasyPaisa"},
{id:2,name:"Women Dress 1",category:"Women",type:"Dress",price:1500,img:"https://images.unsplash.com/photo-1600180758895-02b1ffb83d24?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=400",payment:"JazzCash"},
{id:3,name:"Kids Jacket 1",category:"Kids",type:"Jacket",price:1800,img:"https://images.unsplash.com/photo-1602810319687-80f75dcbfc92?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=400",payment:"Bank Transfer"},
// Continue 50+ products with proper images...
];

// Cart
let cart=JSON.parse(localStorage.getItem("cart")||"[]");

function renderProducts(){
let p=document.getElementById("products");
p.innerHTML="";
products.forEach(prod=>{
p.innerHTML+=`<div class="card">
<img src="${prod.img}">
<h4>${prod.name}</h4>
<div class="cat">${prod.category} - ${prod.type}</div>
<div class="price">PKR ${prod.price}</div>
<button onclick='addToCart(${JSON.stringify(prod)})'>Add to Cart</button>
</div>`});
updateCart();
}

function addToCart(prod){cart.push(prod);localStorage.setItem("cart",JSON.stringify(cart));updateCart();updatePaymentOptions();}
function updateCart(){document.getElementById("cartCount").innerText=cart.length;let box=document.getElementById("cartItems"); box.innerHTML="";let total=0;cart.forEach(i=>{total+=i.price;box.innerHTML+=`<div class="cart-item">${i.name} - ${i.price} PKR</div>`});document.getElementById("total").innerText=total;}
function toggleCart(){let c=document.getElementById("cartBox");c.style.display=c.style.display=="block"?"none":"block";updatePaymentOptions();updateCart();}
function updatePaymentOptions(){let pay=document.getElementById("payment");pay.innerHTML="";let uniqueMethods=[...new Set(cart.map(c=>c.payment))];uniqueMethods.forEach(m=>{let opt=document.createElement("option");opt.value=m; opt.innerText=m;pay.appendChild(opt);});if(uniqueMethods.length==0){let opt=document.createElement("option");opt.value="EasyPaisa"; opt.innerText="EasyPaisa";pay.appendChild(opt);}}

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

// Social
function orderSocial(platform){
if(cart.length==0){alert("Cart empty!"); return;}
let msg=platform+" ORDER%0A";cart.forEach(i=>msg+=`${i.name} - ${i.price} PKR - Payment: ${i.payment}%0A`);
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

// Auth
function signup(){const email=document.getElementById("email").value;const pass=document.getElementById("password").value;createUserWithEmailAndPassword(auth,email,pass).then(userCred=>{sendEmailVerification(userCred.user).then(()=>{document.getElementById("authMsg").innerText="Verification email sent!"})}).catch(err=>{document.getElementById("authMsg").innerText=err.message});}
function login(){const email=document.getElementById("email").value;const pass=document.getElementById("password").value;signInWithEmailAndPassword(auth,email,pass).then(userCred=>{if(!userCred.user.emailVerified){alert("Verify email first!");return;}document.getElementById("authDiv").style.display="none";document.getElementById("userDiv").style.display="block";document.getElementById("userEmail").innerText=userCred.user.email;}).catch(err=>{document.getElementById("authMsg").innerText=err.message});}
function logout(){signOut(auth).then(()=>{document.getElementById("authDiv").style.display="block";document.getElementById("userDiv").style.display="none";});}
onAuthStateChanged(auth,user=>{if(user && user.emailVerified){document.getElementById("authDiv").style.display="none";document.getElementById("userDiv").style.display="block";document.getElementById("userEmail").innerText=user.email;}else{document.getElementById("authDiv").style.display="block";document.getElementById("userDiv").style.display="none";}});

// Admin
function adminLogin(){const pass=document.getElementById("adminPass").value;if(pass===ADMIN_PASS){document.getElementById("adminDiv").style.display="none";document.getElementById("adminPanel").style.display="block";loadOrders();}else{document.getElementById("adminMsg").innerText="Wrong password!"}}
function logoutAdmin(){document.getElementById("adminPanel").style.display="none";document.getElementById("adminDiv").style.display="block";}
function addProduct(){const newProd={id:Date.now(),name:pName.value,category:pCategory.value,type:pType.value,price:Number(pPrice.value),img:pImg.value,payment:pPayment.value};products.push(newProd);renderProducts();pName.value=pCategory.value=pType.value=pPrice.value=pImg.value="";alert("Product added!");}
function loadOrders(){const ordersRef=ref(db,'orders');onValue(ordersRef,snapshot=>{const ordersDiv=document.getElementById("adminOrders");ordersDiv.innerHTML="";snapshot.forEach(snap=>{const val=snap.val();ordersDiv.innerHTML+=`<div style="border-bottom:1px solid #333;padding:5px;"><b>${val.email}</b>: Total ${val.total} PKR</div>`});});}

renderProducts();
</script>
</body>
</html>
