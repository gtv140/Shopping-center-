<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Demo Online Shop</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>
body{margin:0;font-family:Arial;background:#f2f2f2}
header{background:#111;color:#fff;padding:15px;text-align:center}
.container{max-width:1200px;margin:auto;padding:15px}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:15px}
.card{background:#fff;padding:10px;border-radius:10px;box-shadow:0 2px 6px rgba(0,0,0,.1)}
.card img{width:100%;height:180px;object-fit:cover;border-radius:8px}
.price{color:#e63946;font-weight:bold;font-size:18px}
button{background:#25d366;color:#fff;border:none;padding:10px;border-radius:6px;width:100%;cursor:pointer}
footer{text-align:center;color:#555;padding:15px}
.cart{background:#111;color:#fff;padding:10px;border-radius:8px;margin-top:15px}
</style>
</head>

<body>

<header>
<h2>Fashion & Accessories Shop</h2>
<p>Quality Products • Best Prices</p>
</header>

<div class="container">

<div class="products" id="products"></div>

<div class="cart">
<h3>Cart</h3>
<div id="cart"></div>
<button onclick="checkout()">Order on WhatsApp</button>
</div>

</div>

<footer>
© 2026 Demo Shop | 100% Trusted
</footer>

<script>
let products=[
{
 name:"Men Casual Watch",
 price:2999,
 img:"https://images.unsplash.com/photo-1523275335684-37898b6baf30",
 desc:"Stylish casual watch for men. Premium quality."
},
{
 name:"Wireless Bluetooth Headphones",
 price:4499,
 img:"https://images.unsplash.com/photo-1505740420928-5e560c06d30e",
 desc:"Noise reduction, long battery life."
},
{
 name:"Women Leather Handbag",
 price:3899,
 img:"https://images.unsplash.com/photo-1584917865442-de89df76afd3",
 desc:"Elegant handbag for daily use."
},
{
 name:"Running Shoes",
 price:5599,
 img:"https://images.unsplash.com/photo-1542291026-7eec264c27ff",
 desc:"Comfortable & durable sports shoes."
},
{
 name:"Smart Fitness Band",
 price:2499,
 img:"https://images.unsplash.com/photo-1511707171634-5f897ff02aa9",
 desc:"Track steps, heart rate & sleep."
},
{
 name:"Sunglasses",
 price:1999,
 img:"https://images.unsplash.com/photo-1511499767150-a48a237f0083",
 desc:"UV protection stylish sunglasses."
}
];

let cart=[];

function renderProducts(){
 document.getElementById("products").innerHTML=
 products.map((p,i)=>`
 <div class="card">
  <img src="${p.img}">
  <h4>${p.name}</h4>
  <p>${p.desc}</p>
  <div class="price">Rs. ${p.price}</div>
  <button onclick="addCart(${i})">Add to Cart</button>
 </div>
 `).join("");
}

function addCart(i){
 cart.push(products[i]);
 document.getElementById("cart").innerHTML=
 cart.map(c=>`${c.name} - Rs.${c.price}`).join("<br>");
}

function checkout(){
 let msg=cart.map(c=>c.name+" Rs."+c.price).join("%0A");
 window.open("https://wa.me/923000000000?text=Order%0A"+msg);
}

renderProducts();
</script>

</body>
</html>
