<html>
<head>
<meta charset="UTF-8">
<title>Real Online Store</title>

<style>
body{margin:0;font-family:Arial;background:#f4f4f4}
header{background:#111;color:#fff;padding:15px;text-align:center}
.search{padding:10px}
.search input{width:100%;padding:10px}
.collections{display:flex;gap:10px;padding:10px;flex-wrap:wrap}
.collections button{padding:8px;border:none;background:#ddd;cursor:pointer}
.products{display:flex;flex-wrap:wrap;gap:15px;padding:15px}
.card{background:#fff;width:200px;border-radius:8px;box-shadow:0 2px 5px rgba(0,0,0,.2);padding:10px}
.card img{width:100%;height:140px;object-fit:cover}
button{background:#28a745;color:#fff;border:none;padding:8px;width:100%;border-radius:5px;cursor:pointer}
#cart{background:#fff;padding:15px;margin:15px;border-radius:8px}
input,select{width:100%;padding:8px;margin:5px 0}
footer{background:#111;color:#fff;text-align:center;padding:10px}
</style>
</head>

<body>

<header>
<h2>Real Online Store</h2>
<p>Trusted | Fast | Secure</p>
</header>

<div class="search">
<input id="search" placeholder="Search products..." onkeyup="renderProducts()">
</div>

<div class="collections">
<button onclick="filterCat('All')">All</button>
<button onclick="filterCat('Shoes')">Shoes</button>
<button onclick="filterCat('Clothes')">Clothes</button>
<button onclick="filterCat('Electronics')">Electronics</button>
</div>

<div class="products" id="products"></div>

<div id="cart">
<h3>Cart</h3>
<ul id="cartItems"></ul>
<h4>Total: <span id="total">0</span> PKR</h4>

<h3>Checkout</h3>
<input id="name" placeholder="Name">
<input id="phone" placeholder="WhatsApp Number">
<input id="email" placeholder="Email">

<select id="payment">
<option>EasyPaisa</option>
<option>JazzCash</option>
<option>Bank Transfer</option>
</select>

<p>
<b>Payment Info (Edit Yourself)</b><br>
EasyPaisa: 03XXXXXXXXX<br>
JazzCash: 03XXXXXXXXX<br>
Bank IBAN HERE
</p>

<input id="trx" placeholder="Transaction ID">

<button onclick="placeOrder()">Place Order</button>
</div>

<footer>© 2026 Real Store</footer>

<script>
let categories=["Shoes","Clothes","Electronics"];
let products=[];
for(let i=1;i<=50;i++){
 products.push({
  name:"Product "+i,
  price:1000+(i*50),
  cat:categories[i%3],
  img:"https://picsum.photos/300/200?random="+i
 });
}

let cart=JSON.parse(localStorage.getItem("cart"))||[];
let currentCat="All";

function filterCat(cat){currentCat=cat;renderProducts();}

function renderProducts(){
 let p=document.getElementById("products");
 let s=document.getElementById("search").value.toLowerCase();
 p.innerHTML="";
 products.filter(x=>
  (currentCat=="All"||x.cat==currentCat)&&
  x.name.toLowerCase().includes(s)
 ).forEach(x=>{
  p.innerHTML+=`
   <div class="card">
    <img src="${x.img}">
    <h4>${x.name}</h4>
    <p>${x.cat}</p>
    <p>${x.price} PKR</p>
    <button onclick="addToCart('${x.name}',${x.price})">Add</button>
   </div>`;
 });
}

function addToCart(n,p){
 cart.push({n,p});
 localStorage.setItem("cart",JSON.stringify(cart));
 renderCart();
}

function renderCart(){
 let ul=document.getElementById("cartItems");
 let t=0; ul.innerHTML="";
 cart.forEach(i=>{
  t+=i.p;
  ul.innerHTML+=`<li>${i.n} - ${i.p} PKR</li>`;
 });
 document.getElementById("total").innerText=t;
}
renderProducts(); renderCart();

function placeOrder(){
 let msg="Order%0A";
 cart.forEach(i=>msg+=i.n+" - "+i.p+" PKR%0A");
 msg+="Total: "+total.innerText+" PKR%0A";
 msg+="Name: "+name.value+"%0A";
 msg+="Phone: "+phone.value+"%0A";
 msg+="Payment: "+payment.value+"%0A";
 msg+="TRX: "+trx.value;
 window.open("https://wa.me/92XXXXXXXXX?text="+msg);
}
</script>

</body>
</html>
