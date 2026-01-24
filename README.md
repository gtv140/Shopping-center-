<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Full Shop Demo</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{margin:0;font-family:Arial;background:#f4f4f4}
header{background:#111;color:#fff;padding:15px;text-align:center}
.container{max-width:1200px;margin:auto;padding:15px}
.flex{display:flex;gap:10px;flex-wrap:wrap}
input,textarea,button{padding:10px;border-radius:6px;border:1px solid #ccc}
button{cursor:pointer}
.admin, .shop{background:#fff;padding:15px;border-radius:10px;margin-bottom:20px}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:15px}
.card{background:#fff;padding:10px;border-radius:10px;box-shadow:0 2px 6px rgba(0,0,0,.1)}
.card img{width:100%;height:160px;object-fit:cover;border-radius:8px}
.price{color:#e63946;font-weight:bold}
.cart{background:#111;color:#fff;padding:10px;border-radius:8px;margin-top:10px}
footer{text-align:center;color:#555;padding:10px}
</style>
</head>

<body>

<header>
<h1>Client Online Shop (Full Demo)</h1>
<p>Admin + Shop + Cart + LocalStorage</p>
</header>

<div class="container">

<!-- ADMIN PANEL -->
<div class="admin">
<h2>Admin Panel (Client Use)</h2>
<div class="flex">
<input id="pname" placeholder="Product Name">
<input id="pprice" placeholder="Price">
<input id="pimg" placeholder="Image URL">
</div>
<textarea id="pdesc" placeholder="Description"></textarea>
<br><br>
<button onclick="addProduct()">Add Product</button>
</div>

<!-- SEARCH -->
<input id="search" placeholder="Search product..." onkeyup="renderProducts()">

<!-- SHOP -->
<div class="shop">
<h2>Shop</h2>
<div class="products" id="products"></div>
</div>

<!-- CART -->
<div class="cart">
<h3>Cart</h3>
<div id="cart"></div>
<button onclick="checkout()">Order on WhatsApp</button>
</div>

</div>

<footer>© 2026 Full Shop Demo</footer>

<script>
let products = JSON.parse(localStorage.getItem("products")) || [
 {name:"Demo Product",price:1500,img:"https://images.unsplash.com/photo-1523275335684-37898b6baf30",desc:"Sample product"}
];
let cart=[];

function save(){localStorage.setItem("products",JSON.stringify(products));}

function addProduct(){
 let p={name:pname.value,price:pprice.value,img:pimg.value,desc:pdesc.value};
 products.push(p); save(); renderProducts();
 pname.value=pprice.value=pimg.value=pdesc.value="";
}

function renderProducts(){
 let s=search.value.toLowerCase();
 productsDiv=products.filter(p=>p.name.toLowerCase().includes(s))
 .map((p,i)=>`
  <div class="card">
   <img src="${p.img}">
   <h3>${p.name}</h3>
   <p>${p.desc}</p>
   <div class="price">Rs. ${p.price}</div>
   <button onclick="addCart(${i})">Add to Cart</button>
   <button onclick="del(${i})">Delete</button>
  </div>`).join("");
 document.getElementById("products").innerHTML=productsDiv;
}

function del(i){products.splice(i,1);save();renderProducts();}

function addCart(i){cart.push(products[i]);renderCart();}

function renderCart(){
 document.getElementById("cart").innerHTML=
 cart.map(c=>`${c.name} - Rs.${c.price}`).join("<br>");
}

function checkout(){
 let msg=cart.map(c=>c.name+" Rs."+c.price).join("%0A");
 window.open("https://wa.me/923000000000?text=Order:%0A"+msg);
}

renderProducts();
</script>

</body>
</html>
