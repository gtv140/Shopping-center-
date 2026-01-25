<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body{margin:0;font-family:Arial,sans-serif;background:#f5f5f5;color:#111}
header{padding:20px;text-align:center;background:#111;color:#fff;}
header h1{margin:0;font-size:32px;}
header p{margin:5px;font-size:16px;color:#ccc;}
.offers-slider{display:flex;overflow-x:auto;gap:10px;padding:10px;background:#222;color:#fff;}
.offers-slider div{min-width:220px;padding:15px;background:#ff003c;border-radius:10px;flex-shrink:0;text-align:center;animation:slideOffers 20s linear infinite;}
@keyframes slideOffers{0%{transform:translateX(0);}100%{transform:translateX(-50%);}}
.search-bar{display:flex;flex-wrap:wrap;justify-content:center;padding:10px;background:#fff;}
.search-bar input, .search-bar select, .search-bar button{padding:8px;margin:5px;border-radius:6px;border:1px solid #ccc;}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:20px;padding:20px;}
.card{background:#fff;padding:15px;border-radius:10px;box-shadow:0 4px 12px rgba(0,0,0,0.15);transition:.3s;}
.card:hover{transform:scale(1.05);box-shadow:0 8px 20px rgba(0,0,0,0.2);}
.card img{width:100%;height:180px;object-fit:cover;border-radius:8px;}
.card h4{margin:8px 0 5px;font-size:17px;color:#111;}
.card .desc{font-size:14px;color:#555;margin:4px 0;}
.card .price{color:#0077cc;font-weight:bold;margin:6px 0;}
.card button{padding:10px;border:none;border-radius:6px;background:#0077cc;color:#fff;cursor:pointer;width:100%;transition:.3s;}
.card button:hover{background:#ff003c;}
#cartBtn{position:fixed;bottom:20px;right:20px;padding:15px;border-radius:50%;background:#ff003c;color:#fff;font-size:20px;cursor:pointer;}
#cartBox{display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.8);z-index:999;overflow:auto;}
#cart{background:#fff;margin:40px auto;padding:20px;border-radius:12px;max-width:500px;color:#111;}
.cart-item{display:flex;justify-content:space-between;margin:8px 0;border-bottom:1px solid #ddd;}
footer{text-align:center;padding:15px;background:#111;color:#fff;font-size:14px;}
input,select{width:100%;padding:8px;margin:5px 0;border-radius:6px;border:1px solid #ccc;}
.social-icons{display:flex;gap:15px;margin-top:10px;}
.social-icons a{color:#111;font-size:20px;text-decoration:none;}
</style>
</head>
<body>

<header>
<h1>Shopping Center</h1>
<p>Best Online Store | Offers • Trending • Fast Checkout</p>
</header>

<div class="offers-slider">
<div>🔥 50% OFF on Men’s Wear!</div>
<div>✨ Women’s Fashion – Flat 30% OFF!</div>
<div>🎁 Free Delivery on Orders Above PKR 5000!</div>
<div>💳 JazzCash Cashback Offers Live!</div>
</div>

<div class="search-bar">
<input type="text" id="searchInput" placeholder="Search products...">
<select id="filterCategory">
<option value="All">All Categories</option>
<option value="Men">Men</option>
<option value="Women">Women</option>
<option value="Kids">Kids</option>
<option value="Electronics">Electronics</option>
<option value="Accessories">Accessories</option>
</select>
<select id="sortOption">
<option value="none">Sort By</option>
<option value="priceLow">Price: Low to High</option>
<option value="priceHigh">Price: High to Low</option>
<option value="nameAZ">Name: A‑Z</option>
<option value="nameZA">Name: Z‑A</option>
</select>
<button onclick="applyFilters()">Apply</button>
</div>

<div class="products" id="products"></div>

<button id="cartBtn" onclick="toggleCart()">🛒 Cart (<span id="cartCount">0</span>)</button>

<div id="cartBox">
<div id="cart">
<h3>Your Cart</h3>
<div id="cartItems"></div>
<h4>Total: <span id="total">0</span> PKR</h4>
<h3>Checkout</h3>
<input id="c_name" placeholder="Full Name">
<input id="c_phone" placeholder="WhatsApp Number">
<input id="c_address" placeholder="Delivery Address">
<input id="c_email" placeholder="Email">
<select id="payment">
<option>EasyPaisa</option>
<option>JazzCash</option>
<option>Cash on Delivery</option>
<option>Bank Transfer</option>
</select>
<input id="trx" placeholder="Transaction ID (if paid)">
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

<footer>Shopping Center © 2026 All Rights Reserved</footer>

<script>
// Full 50+ products
let products=[
{id:1,name:"Men Casual Shirt",category:"Men",type:"Shirt",price:1199,img:"https://images.pexels.com/photos/428338/pexels-photo-428338.jpeg?auto=compress&cs=tinysrgb&w=400",desc:"Classic men’s casual shirt for everyday wear."},
{id:2,name:"Women Summer Dress",category:"Women",type:"Dress",price:1499,img:"https://images.pexels.com/photos/296896/pexels-photo-296896.jpeg?auto=compress&cs=tinysrgb&w=400",desc:"Lightweight summer dress, stylish fit."},
{id:3,name:"Kids Winter Jacket",category:"Kids",type:"Jacket",price:1799,img:"https://images.pexels.com/photos/163097/fashion-children-boy-girl-163097.jpeg?auto=compress&cs=tinysrgb&w=400",desc:"Warm and cozy winter jacket for kids."},
{id:4,name:"Men Formal Shirt",category:"Men",type:"Shirt",price:1299,img:"https://images.pexels.com/photos/428338/pexels-photo-428338.jpeg?auto=compress&cs=tinysrgb&w=400",desc:"Slim fit formal shirt excellent for office wear."},
{id:5,name:"Women Handbag",category:"Accessories",type:"Bag",price:1899,img:"https://images.pexels.com/photos/769289/pexels-photo-769289.jpeg?auto=compress&cs=tinysrgb&w=400",desc:"Fashionable handbag with premium finish."},
{id:6,name:"Wireless Earbuds",category:"Electronics",type:"Earbuds",price:2999,img:"https://images.pexels.com/photos/3394664/pexels-photo-3394664.jpeg?auto=compress&cs=tinysrgb&w=400",desc:"High quality wireless earbuds with mic."},
{id:7,name:"Men Running Shoes",category:"Men",type:"Shoes",price:2499,img:"https://images.pexels.com/photos/2529148/pexels-photo-2529148.jpeg?auto=compress&cs=tinysrgb&w=400",desc:"Comfortable running shoes for daily workouts."},
{id:8,name:"Women Sandals",category:"Women",type:"Shoes",price:1599,img:"https://images.pexels.com/photos/298863/pexels-photo-298863.jpeg?auto=compress&cs=tinysrgb&w=400",desc:"Stylish sandals perfect for summer."},
{id:9,name:"Kids Toy Set",category:"Kids",type:"Toys",price:1299,img:"https://images.pexels.com/photos/207983/pexels-photo-207983.jpeg?auto=compress&cs=tinysrgb&w=400",desc:"Fun toy set to keep kids entertained."},
{id:10,name:"Smartwatch",category:"Electronics",type:"Watch",price:3999,img:"https://images.pexels.com/photos/267394/pexels-photo-267394.jpeg?auto=compress&cs=tinysrgb&w=400",desc:"Smartwatch with multiple fitness features."},
// Add remaining products up to 50+ with real images and details
];

let cart=JSON.parse(localStorage.getItem("cart")||"[]");

function renderProducts(list=products){
let p=document.getElementById("products"), html="";
list.forEach(prod=>{
html+=`<div class="card">
<img src="${prod.img}">
<h4>${prod.name}</h4>
<div class="cat">${prod.category} - ${prod.type}</div>
<div class="desc">${prod.desc}</div>
<div class="price">PKR ${prod.price}</div>
<button onclick='addToCart(${JSON.stringify(prod)})'>Add to Cart</button>
</div>`;
});
p.innerHTML=html;
updateCart();
}

function addToCart(prod){cart.push(prod);localStorage.setItem("cart",JSON.stringify(cart));updateCart();}
function updateCart(){document.getElementById("cartCount").innerText=cart.length;let t=0, box=document.getElementById("cartItems");box.innerHTML="";cart.forEach(i=>{t+=i.price;box.innerHTML+=`<div class="cart-item">${i.name} - PKR ${i.price}</div>`});document.getElementById("total").innerText=t;}
function toggleCart(){let box=document.getElementById("cartBox");box.style.display=box.style.display=="block"?"none":"block";updateCart();}
function placeOrder(){if(cart.length==0){alert("Cart empty!");return;}alert("Order placed!");cart=[];localStorage.setItem("cart",JSON.stringify(cart));updateCart();toggleCart();}
function orderSocial(platform){if(cart.length==0){alert("Cart empty!");return;}let msg=platform+" ORDER\n";cart.forEach(i=>msg+=`${i.name} - ${i.price} PKR\n`);msg+=`\nName: ${c_name.value}\nPhone: ${c_phone.value}\nAddress: ${c_address.value}\nPayment: ${payment.value}`;let url="";switch(platform){case"WhatsApp":url="https://wa.me/92XXXXXXXXX?text="+encodeURIComponent(msg);break;case"Email":url="mailto:example@email.com?subject=Order&body="+encodeURIComponent(msg);break;case"Instagram":url="https://instagram.com/direct/inbox?text="+encodeURIComponent(msg);break;case"Facebook":url="https://www.facebook.com/messages/t/?message="+encodeURIComponent(msg);break;}window.open(url,"_blank");}

function applyFilters(){
let kw=document.getElementById("searchInput").value.toLowerCase();
let cat=document.getElementById("filterCategory").value;
let sort=document.getElementById("sortOption").value;
let filtered=products.filter(p=> (p.name.toLowerCase().includes(kw) || p.desc.toLowerCase().includes(kw)) && (cat=="All"||p.category==cat));
if(sort=="priceLow") filtered.sort((a,b)=>a.price-b.price);
if(sort=="priceHigh") filtered.sort((a,b)=>b.price-a.price);
if(sort=="nameAZ") filtered.sort((a,b)=>a.name.localeCompare(b.name));
if(sort=="nameZA") filtered.sort((a,b)=>b.name.localeCompare(a.name));
renderProducts(filtered);
}

renderProducts();
</script>
</body>
</html>
