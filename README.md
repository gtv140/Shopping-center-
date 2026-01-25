<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>
<style>
body{margin:0;font-family:Arial;background:#0b0b0b;color:#fff}
header{padding:25px;text-align:center;background:#111}
header h1{margin:0;font-size:32px}
header p{margin:5px;font-size:16px;color:#ccc}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:20px;padding:20px}
.card{background:#111;padding:10px;border-radius:12px;box-shadow:0 0 15px #ff003c;transition:.3s;position:relative}
.card:hover{transform:scale(1.05);box-shadow:0 0 25px #1e90ff}
.card img{width:100%;height:180px;object-fit:cover;border-radius:10px}
.card h4{margin:5px 0;font-size:16px;color:#ff003c}
.card .cat{font-size:14px;color:#ccc}
.price{color:#00ffcc;font-weight:bold;margin:5px 0}
.card button{padding:10px;width:100%;border:none;border-radius:6px;background:#1e90ff;color:#fff;cursor:pointer;margin-top:5px;transition:.3s}
.card button:hover{background:#ff003c}
#cartBtn{position:fixed;bottom:20px;right:20px;padding:15px;border-radius:50%;background:#ff003c;color:#fff;font-size:20px;cursor:pointer;animation:neonGlow 2s infinite alternate}
#cartBox{display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:#000c;z-index:99;overflow:auto}
#cart{background:#111;margin:40px auto;padding:20px;border-radius:12px;max-width:450px}
.cart-item{display:flex;justify-content:space-between;margin:6px 0;border-bottom:1px solid #333;padding-bottom:4px}
.social-icons{display:flex;gap:15px;margin-top:10px}
.social-icons a{color:#fff;text-decoration:none;font-size:20px;transition:.3s}
.social-icons a:hover{color:#ff003c}
.features{background:#111;padding:15px;margin:20px;border-radius:12px;box-shadow:0 0 15px #1e90ff}
.features ul{padding-left:20px}
footer{text-align:center;padding:15px;background:#111;color:#fff;font-size:14px;box-shadow:0 -2px 10px #ff003c}
@keyframes neonGlow{0%{box-shadow:0 0 5px #ff003c,0 0 10px #1e90ff;}50%{box-shadow:0 0 15px #ff003c,0 0 25px #1e90ff;}100%{box-shadow:0 0 5px #ff003c,0 0 10px #1e90ff;}}
</style>
</head>
<body>

<header>
<h1>Shopping Center</h1>
<p>Premium Neon Animated Store</p>
</header>

<div class="features">
<h3>Why Shop With Us?</h3>
<ul>
<li>50+ Trending Products for Men, Women & Kids</li>
<li>Secure & Fast Payment Options (EasyPaisa, JazzCash, Bank Transfer)</li>
<li>Buy Now & Checkout Directly</li>
<li>Social Share: WhatsApp, Email, Instagram, Facebook</li>
<li>Exclusive Offers & Discounts</li>
<li>Premium Neon Animated Visuals</li>
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
<select id="payment">
<option>EasyPaisa</option>
<option>JazzCash</option>
<option>Bank Transfer</option>
</select>
<input id="trx" placeholder="Transaction ID">
<div class="social-icons">
<a href="#" onclick="orderSocial('WhatsApp')">📱 WhatsApp</a>
<a href="#" onclick="orderSocial('Email')">✉️ Email</a>
<a href="#" onclick="orderSocial('Instagram')">📸 Instagram</a>
<a href="#" onclick="orderSocial('Facebook')">📘 Facebook</a>
</div>
<button onclick="placeOrder()">Place Order</button>
<button onclick="toggleCart()">Close</button>
</div>
</div>

<footer>Shopping Center © 2026 - All Rights Reserved</footer>

<script>
// Products with curated images
let products=[
{id:1,name:"Men Shirt 1",category:"Men",type:"Shirt",price:1200,img:"https://images.pexels.com/photos/428338/pexels-photo-428338.jpeg?auto=compress&cs=tinysrgb&w=400",payment:"EasyPaisa"},
{id:2,name:"Women Dress 1",category:"Women",type:"Dress",price:1500,img:"https://images.pexels.com/photos/296896/pexels-photo-296896.jpeg?auto=compress&cs=tinysrgb&w=400",payment:"JazzCash"},
{id:3,name:"Kids Jacket 1",category:"Kids",type:"Jacket",price:1800,img:"https://images.pexels.com/photos/163097/fashion-children-boy-girl-163097.jpeg?auto=compress&cs=tinysrgb&w=400",payment:"Bank Transfer"},
// Add more 50+ products
];

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

function addToCart(prod){cart.push(prod);localStorage.setItem("cart",JSON.stringify(cart));updateCart();}
function updateCart(){document.getElementById("cartCount").innerText=cart.length;let total=0;let box=document.getElementById("cartItems");box.innerHTML="";cart.forEach(i=>{total+=i.price;box.innerHTML+=`<div class="cart-item">${i.name} - ${i.price} PKR</div>`});document.getElementById("total").innerText=total;}

function toggleCart(){let c=document.getElementById("cartBox");c.style.display=c.style.display=="block"?"none":"block";updateCart();}

function placeOrder(){if(cart.length==0){alert("Cart empty!");return;}alert("Order placed!");cart=[];localStorage.setItem("cart",JSON.stringify(cart));updateCart();toggleCart();}

function orderSocial(platform){if(cart.length==0){alert("Cart empty!");return;}let msg=platform+" ORDER\n";cart.forEach(i=>msg+=`${i.name} - ${i.price} PKR - Payment: ${i.payment}\n`);msg+=`Total: ${document.getElementById("total").innerText} PKR\nName: ${c_name.value}\nPhone: ${c_phone.value}\nPayment: ${payment.value}\nTRX: ${trx.value}`;let url="";switch(platform){case"WhatsApp":url="https://wa.me/92XXXXXXXXX?text="+encodeURIComponent(msg);break;case"Email":url="mailto:example@email.com?subject=Order&body="+encodeURIComponent(msg);break;case"Instagram":url="https://instagram.com/direct/inbox?text="+encodeURIComponent(msg);break;case"Facebook":url="https://www.facebook.com/messages/t/?message="+encodeURIComponent(msg);break;}window.open(url,"_blank");}

renderProducts();
</script>
</body>
</html>
