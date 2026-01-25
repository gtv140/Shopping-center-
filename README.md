<html>
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>
<style>
body{margin:0;font-family:Arial;background:#0b0b0b;color:#fff}
header{padding:15px;text-align:center;background:linear-gradient(90deg,#ff003c,#1e90ff);box-shadow:0 0 15px #ff003c}
header h1{margin:0}
.topbar{display:flex;justify-content:center;gap:10px;padding:10px;flex-wrap:wrap}
.topbar input,select{padding:8px;border-radius:6px;border:none;min-width:150px}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:15px;padding:15px}
.card{background:#111;padding:10px;border-radius:10px;box-shadow:0 0 10px #ff003c;transition:.3s;position:relative}
.card:hover{transform:scale(1.05)}
.card img{width:100%;height:180px;object-fit:cover;border-radius:8px}
.price{color:#00ffcc;font-weight:bold;margin:6px 0}
button{padding:8px;border:none;border-radius:6px;background:#ff003c;color:#fff;cursor:pointer;margin-top:5px}
button.secondary{background:#1e90ff}
#cartBtn{position:fixed;bottom:20px;right:20px;padding:12px;border-radius:50%;background:#1e90ff;cursor:pointer}
#cartBox{display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:#000c;z-index:9;overflow:auto}
#cart{background:#111;margin:40px auto;padding:15px;border-radius:10px;max-width:400px}
.cart-item{display:flex;justify-content:space-between;margin:6px 0;border-bottom:1px solid #333;padding-bottom:4px}
input,select{width:100%;padding:8px;margin:5px 0;border-radius:6px;border:none}
footer{text-align:center;padding:10px;background:#111;color:#fff;font-size:14px}
</style>
</head>
<body>

<header>
<h1>Shopping Center</h1>
<p>Premium Online Store</p>
</header>

<div class="topbar">
<input id="search" placeholder="Search products..." onkeyup="render()">
<select id="category" onchange="render()">
<option value="">All Categories</option>
<option>Men</option>
<option>Women</option>
<option>Kids</option>
<option>Winter</option>
<option>Accessories</option>
<option>Electronics</option>
<option>Shoes</option>
</select>
<select id="sort" onchange="render()">
<option value="">Sort</option>
<option value="low">Price: Low to High</option>
<option value="high">Price: High to Low</option>
</select>
<button onclick="toggleCart()">Cart 🛒 (<span id="cartCount">0</span>)</button>
</div>

<div class="products" id="products"></div>

<div id="cartBox">
<div id="cart">
<h3>Your Cart</h3>
<div id="cartItems"></div>
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
<b>Payment placeholders (edit yourself):</b><br>
EasyPaisa: 03XXXXXXXXX<br>
JazzCash: 03XXXXXXXXX<br>
Bank IBAN HERE
</p>
<input id="trx" placeholder="Transaction ID">
<button onclick="placeOrder()">Place Order</button>
<button class="secondary" onclick="toggleCart()">Close</button>
</div>
</div>

<footer>
Order via Email / Instagram / Facebook / WhatsApp
</footer>

<script>
let categories=["Men","Women","Kids","Winter","Accessories","Electronics","Shoes"];
let products=[];
for(let i=1;i<=50;i++){
products.push({
id:i,
name:`Product ${i}`,
category:categories[i%categories.length],
price:1000+(i*50),
img:`https://source.unsplash.com/400x300/?${i},product`
});
}

let cart=JSON.parse(localStorage.getItem("cart")||"[]");

function render(){
let q=document.getElementById("search").value.toLowerCase();
let c=document.getElementById("category").value;
let s=document.getElementById("sort").value;
let p=document.getElementById("products");
let list=products.filter(x=>
 (c==""||x.category==c)&&
 x.name.toLowerCase().includes(q)
);
if(s=="low") list.sort((a,b)=>a.price-b.price);
if(s=="high") list.sort((a,b)=>b.price-a.price);
p.innerHTML="";
list.forEach(x=>{
p.innerHTML+=`
<div class="card">
<img src="${x.img}">
<h4>${x.name}</h4>
<div>${x.category}</div>
<div class="price">PKR ${x.price}</div>
<button onclick='addToCart(${JSON.stringify(x)})'>Add to Cart</button>
</div>`;
});
updateCart();
}

function addToCart(p){cart.push(p);save();updateCart();}
function updateCart(){
document.getElementById("cartCount").innerText=cart.length;
let box=document.getElementById("cartItems");box.innerHTML="";
let total=0;
cart.forEach(i=>{
total+=i.price;
box.innerHTML+=`<div class="cart-item">${i.name} - ${i.price} PKR</div>`;
});
document.getElementById("total").innerText=total;
}
function toggleCart(){let c=document.getElementById("cartBox");c.style.display=c.style.display=="block"?"none":"block";updateCart();}
function save(){localStorage.setItem("cart",JSON.stringify(cart));}
function placeOrder(){
let msg="ORDER DETAILS%0A";
cart.forEach(i=>msg+=`${i.name} - ${i.price} PKR%0A`);
msg+=`Name: ${name.value}%0APhone: ${phone.value}%0APayment: ${payment.value}%0ATRX: ${trx.value}`;
window.open(`https://wa.me/92XXXXXXXXX?text=${msg}`,"_blank");
cart=[];save();toggleCart();
}

render();
</script>

</body>
</html>
