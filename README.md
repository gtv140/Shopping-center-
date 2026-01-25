<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<!-- Firebase SDKs -->
<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-app.js";
import { getFirestore, collection, addDoc } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "AIzaSyAL7_6DTdz14ySlLQ1jjuQC4WdO4mpRZKY",
  authDomain: "shopping-center-9.firebaseapp.com",
  projectId: "shopping-center-9",
  storageBucket: "shopping-center-9.firebasestorage.app",
  messagingSenderId: "33427127023",
  appId: "1:33427127023:web:a478af6499f28f84d9391a"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

window.saveOrderToFirebase = async function(order){
  try{
    await addDoc(collection(db, "orders"), order);
    alert("Order saved successfully!");
  }catch(e){
    alert("Error saving order: "+e);
  }
}
</script>

<style>
body{margin:0;font-family:Arial,sans-serif;background:#f5f5f5;color:#111;}
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
// 50+ products array
const products = [
  {id:1,name:"Men Casual Shirt",category:"Men",price:1200,desc:"100% Cotton, Slim Fit",img:"https://source.unsplash.com/400x400/?shirt,men"},
  {id:2,name:"Women Summer Dress",category:"Women",price:1500,desc:"Lightweight, Stylish",img:"https://source.unsplash.com/400x400/?dress,women"},
  {id:3,name:"Kids Sneakers",category:"Kids",price:900,desc:"Comfortable and Trendy",img:"https://source.unsplash.com/400x400/?shoes,kids"},
  {id:4,name:"Wireless Earbuds",category:"Electronics",price:2500,desc:"Bluetooth, Noise Cancelling",img:"https://source.unsplash.com/400x400/?earbuds,electronics"},
  {id:5,name:"Leather Wallet",category:"Accessories",price:700,desc:"Genuine Leather",img:"https://source.unsplash.com/400x400/?wallet,accessories"},
  {id:6,name:"Men Formal Shoes",category:"Men",price:2200,desc:"Oxford Style, Leather",img:"https://source.unsplash.com/400x400/?shoes,men"},
  {id:7,name:"Women Handbag",category:"Women",price:1800,desc:"Stylish and Spacious",img:"https://source.unsplash.com/400x400/?handbag,women"},
  {id:8,name:"Kids T-shirt Set",category:"Kids",price:800,desc:"Cotton, 3 pcs pack",img:"https://source.unsplash.com/400x400/?tshirt,kids"},
  {id:9,name:"Smart Watch",category:"Electronics",price:5000,desc:"Fitness Tracker, Stylish",img:"https://source.unsplash.com/400x400/?watch,electronics"},
  {id:10,name:"Sunglasses",category:"Accessories",price:1200,desc:"UV Protection",img:"https://source.unsplash.com/400x400/?sunglasses,accessories"},
  // ...continue until 50+ products
];

// Cart logic
let cart = [];

function renderProducts(list=products){
  const container = document.getElementById("products");
  container.innerHTML="";
  list.forEach(p=>{
    const card = document.createElement("div");
    card.className="card";
    card.innerHTML=`
      <img src="${p.img}" alt="${p.name}">
      <h4>${p.name}</h4>
      <p class="desc">${p.desc}</p>
      <p class="price">${p.price} PKR</p>
      <button onclick="addToCart(${p.id})">Add to Cart</button>
    `;
    container.appendChild(card);
  });
}
renderProducts();

function addToCart(id){
  const product = products.find(p=>p.id===id);
  cart.push(product);
  updateCart();
}

function updateCart(){
  const items = document.getElementById("cartItems");
  const count = document.getElementById("cartCount");
  const totalEl = document.getElementById("total");
  items.innerHTML="";
  let total = 0;
  cart.forEach((p,i)=>{
    const div = document.createElement("div");
    div.className="cart-item";
    div.innerHTML=`${p.name} - ${p.price} PKR <button onclick="removeItem(${i})">Remove</button>`;
    items.appendChild(div);
    total+=p.price;
  });
  count.innerText=cart.length;
  totalEl.innerText=total;
}

function removeItem(index){cart.splice(index,1);updateCart();}
function toggleCart(){
  const box=document.getElementById("cartBox");
  box.style.display=(box.style.display==="none"||box.style.display==="")?"block":"none";
}

function placeOrder(){
  const order={
    name:document.getElementById("c_name").value,
    phone:document.getElementById("c_phone").value,
    address:document.getElementById("c_address").value,
    email:document.getElementById("c_email").value,
    payment:document.getElementById("payment").value,
    trx:document.getElementById("trx").value,
    items:cart
  };
  saveOrderToFirebase(order);
}

function orderSocial(platform){
  alert("Share order on "+platform);
}

function applyFilters(){
  const search=document.getElementById("searchInput").value.toLowerCase();
  const cat=document.getElementById("filterCategory").value;
  const sort=document.getElementById("sortOption").value;
  let filtered = products.filter(p=>p.name.toLowerCase().includes(search));
  if(cat!=="All"){filtered = filtered.filter(p=>p.category===cat);}
  if(sort==="priceLow"){filtered.sort((a,b)=>a.price-b.price);}
  if(sort==="priceHigh"){filtered.sort((a,b)=>b.price-a.price);}
  if(sort==="nameAZ"){filtered.sort((a,b)=>a.name.localeCompare(b.name));}
  if(sort==="nameZA"){filtered.sort((a,b)=>b.name.localeCompare(a.name));}
  renderProducts(filtered);
}
</script>
</body>
</html>
