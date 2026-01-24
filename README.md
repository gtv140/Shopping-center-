<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body{margin:0;font-family:'Segoe UI',sans-serif;background:#f0f4f8}
header{background:linear-gradient(90deg,#ff7e5f,#feb47b);color:#fff;padding:30px;text-align:center;font-size:32px;font-weight:bold;text-shadow:1px 1px #000;letter-spacing:1px}
.container{max-width:1300px;margin:auto;padding:20px}
.flex{display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px}
input,select,button{padding:10px;margin:5px 0;border-radius:8px;border:1px solid #ccc;font-size:14px}
input:focus,select:focus{outline:none;border:2px solid #ff7e5f}
button{cursor:pointer;background:#ff4500;color:#fff;font-weight:bold;transition:0.3s;border:none}
button:hover{opacity:0.9;transform:scale(1.03)}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:20px}
.card{background:#fff;padding:15px;border-radius:15px;box-shadow:0 8px 20px rgba(0,0,0,0.15);transition:0.3s;overflow:hidden;position:relative}
.card:hover{transform:scale(1.05)}
.card img{width:100%;height:180px;object-fit:cover;border-radius:12px;transition:0.3s}
.card h4{margin:10px 0 5px 0;font-size:18px;color:#333}
.card p{font-size:13px;color:#555;margin-bottom:10px;height:40px;overflow:hidden}
.price{color:#ff4500;font-weight:bold;font-size:16px;margin-bottom:10px}
.cart{background:#333;color:#fff;padding:15px;border-radius:12px;margin-top:25px}
footer{text-align:center;color:#555;padding:15px;margin-top:25px;font-size:14px}
.hero{background:linear-gradient(135deg,#6a11cb,#2575fc);color:#fff;padding:40px;text-align:center;border-radius:12px;margin-bottom:20px}
.hero h2{font-size:28px;margin-bottom:10px}
.hero p{font-size:16px}
@media(max-width:768px){.products{grid-template-columns:repeat(auto-fit,minmax(160px,1fr))}}
</style>
</head>
<body>

<header>Shopping Center 🛒</header>

<div class="container">

<!-- HERO / PROMO -->
<div class="hero">
<h2>Welcome to Shopping Center!</h2>
<p>Grab the best deals on top products. Fast delivery & premium quality!</p>
</div>

<!-- SEARCH & CATEGORY -->
<div class="flex">
<input id="search" placeholder="Search products..." onkeyup="renderProducts()">
<select id="filterCat" onchange="renderProducts()">
<option value="">All Categories</option>
<option value="Men">Men</option>
<option value="Women">Women</option>
<option value="Accessories">Accessories</option>
<option value="Electronics">Electronics</option>
<option value="Fitness">Fitness</option>
</select>
</div>

<!-- PRODUCTS -->
<div class="products" id="products"></div>

<!-- CART -->
<div class="cart">
<h3>Your Cart</h3>
<div id="cart"></div>
<select id="payment">
<option>Cash on Delivery</option>
<option>JazzCash</option>
<option>EasyPaisa</option>
</select>
<button onclick="checkout()">Place Order</button>
</div>

</div>

<footer>© 2026 Shopping Center | Premium Deals & Trusted Shop</footer>

<script>
// PRODUCTS LIST
let products=[
{name:"Men Casual Watch",price:2999,img:"https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=300&h=300&fit=crop",desc:"Stylish casual watch for men.",cat:"Men"},
{name:"Wireless Bluetooth Headphones",price:4499,img:"https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=300&h=300&fit=crop",desc:"Noise reduction, long battery life.",cat:"Electronics"},
{name:"Women Leather Handbag",price:3899,img:"https://images.unsplash.com/photo-1584917865442-de89df76afd3?w=300&h=300&fit=crop",desc:"Elegant handbag for daily use.",cat:"Women"},
{name:"Running Shoes",price:5599,img:"https://images.unsplash.com/photo-1542291026-7eec264c27ff?w=300&h=300&fit=crop",desc:"Comfortable & durable sports shoes.",cat:"Men"},
{name:"Smart Fitness Band",price:2499,img:"https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?w=300&h=300&fit=crop",desc:"Track steps, heart rate & sleep.",cat:"Fitness"},
{name:"Sunglasses",price:1999,img:"https://images.unsplash.com/photo-1511499767150-a48a237f0083?w=300&h=300&fit=crop",desc:"UV protection stylish sunglasses.",cat:"Accessories"},
{name:"Casual T-Shirt",price:1499,img:"https://images.unsplash.com/photo-1520975695543-431b42d1a3a7?w=300&h=300&fit=crop",desc:"Comfortable cotton t-shirt.",cat:"Men"},
{name:"Jeans Pants",price:2599,img:"https://images.unsplash.com/photo-1514996937319-344454492b37?w=300&h=300&fit=crop",desc:"Trendy denim jeans.",cat:"Men"},
{name:"Leather Wallet",price:1299,img:"https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?w=300&h=300&fit=crop",desc:"Premium leather wallet.",cat:"Accessories"},
{name:"Sports Cap",price:799,img:"https://images.unsplash.com/photo-1520975919321-2b8f973b5e21?w=300&h=300&fit=crop",desc:"Stylish cap for outdoor.",cat:"Accessories"},
{name:"Women Sneakers",price:3999,img:"https://images.unsplash.com/photo-1600185360833-c9a62753f899?w=300&h=300&fit=crop",desc:"Comfortable sneakers for women.",cat:"Women"},
{name:"Men Formal Shoes",price:4999,img:"https://images.unsplash.com/photo-1580910051074-36ff97893ad9?w=300&h=300&fit=crop",desc:"Elegant formal shoes for men.",cat:"Men"},
{name:"Bluetooth Speaker",price:3299,img:"https://images.unsplash.com/photo-1581276879432-15b9f1c78d5a?w=300&h=300&fit=crop",desc:"Portable wireless speaker.",cat:"Electronics"},
{name:"Women Scarf",price:899,img:"https://images.unsplash.com/photo-1600185360807-38c1b0df063c?w=300&h=300&fit=crop",desc:"Stylish scarf for women.",cat:"Women"},
{name:"Fitness Yoga Mat",price:1299,img:"https://images.unsplash.com/photo-1584467735873-2d63f7e3a2ee?w=300&h=300&fit=crop",desc:"Non-slip yoga mat.",cat:"Fitness"},
{name:"Men Belt",price:699,img:"https://images.unsplash.com/photo-1560377701-607f4ed53b41?w=300&h=300&fit=crop",desc:"Premium leather belt.",cat:"Men"},
{name:"Women Earrings",price:1199,img:"https://images.unsplash.com/photo-1585386959984-a415522f28f7?w=300&h=300&fit=crop",desc:"Elegant earrings for women.",cat:"Women"}
];

let cart=[];

function renderProducts(){
 let searchVal=search.value.toLowerCase();
 let catVal=filterCat.value;
 let filtered=products.filter(p=>p.name.toLowerCase().includes(searchVal)&&(catVal==""||p.cat==catVal));
 document.getElementById("products").innerHTML=filtered.map((p,i)=>`
 <div class="card">
  <img src="${p.img}" loading="lazy">
  <h4>${p.name}</h4>
  <p>${p.desc}</p>
  <div class="price">Rs. ${p.price}</div>
  <button onclick="addCart(${i})">Add to Cart</button>
 </div>`).join("");
}

function addCart(i){
 cart.push(products[i]);
 renderCart();
}

function renderCart(){
 document.getElementById("cart").innerHTML=cart.map(c=>`${c.name} - Rs.${c.price}`).join("<br>");
}

function checkout(){
 if(cart.length==0){alert("Cart is empty"); return;}
 let msg=cart.map(c=>c.name+" Rs."+c.price).join("%0A");
 let paymentMethod=document.getElementById("payment").value;
 msg+="%0A%0APayment Method: "+paymentMethod;
 window.open("https://wa.me/923000000000?text=Order%0A"+msg);
 cart=[];
 renderCart();
}

renderProducts();
renderCart();
</script>

</body>
</html>
