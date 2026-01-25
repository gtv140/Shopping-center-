<html>
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>
<style>
body{margin:0;font-family:Arial;background:#0b0b0b;color:#fff}
header{padding:15px;background:linear-gradient(90deg,#ff003c,#0066ff);text-align:center}
header h1{margin:0}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:15px;padding:15px}
.card{background:#111;border-radius:12px;padding:10px;box-shadow:0 0 10px #000}
.card img{width:100%;height:180px;object-fit:cover;border-radius:10px}
.card h4{margin:8px 0 4px}
.price{color:#00ffcc;font-weight:bold}
button{width:100%;padding:10px;border:none;border-radius:8px;background:#ff003c;color:#fff;cursor:pointer}
button:hover{opacity:.85}

#cartBtn{position:fixed;bottom:20px;right:20px;background:#0066ff;border-radius:50%;width:60px;height:60px;font-size:18px}
#cartBox{display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:#000c;z-index:9}
#cart{background:#111;max-width:420px;margin:40px auto;padding:15px;border-radius:12px}
.cartItem{display:flex;justify-content:space-between;font-size:14px;margin:6px 0}

input,select{width:100%;padding:10px;border-radius:8px;border:none;margin:6px 0}
.secondary{background:#444}
</style>
</head>

<body>

<header>
<h1>🛍 Shopping Center</h1>
<p>Trusted Online Store – Winter Collection</p>
</header>

<div class="grid" id="products"></div>

<button id="cartBtn" onclick="toggleCart()">🛒</button>

<div id="cartBox">
<div id="cart">
<h3>Your Cart</h3>
<div id="cartItems"></div>
<b id="total"></b><br><br>
<button onclick="checkout()">Buy Now</button>
<button class="secondary" onclick="toggleCart()">Close</button>
</div>
</div>

<!-- PAYMENT -->
<div id="paymentBox" style="display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:#000c;z-index:10">
<div style="background:#111;max-width:420px;margin:40px auto;padding:15px;border-radius:12px">
<h3>Payment</h3>

<select id="payMethod">
<option>EasyPaisa</option>
<option>JazzCash</option>
<option>Bank Transfer</option>
</select>

<p>
Send payment to:<br>
<b>0300-1234567</b><br>
Meezan Bank – IBAN: PK00MEZN000000123456
</p>

<input id="txid" placeholder="Transaction ID">

<button onclick="confirmPayment()">Confirm & Send</button>
<button class="secondary" onclick="closePayment()">Cancel</button>
</div>
</div>

<script>
const WHATSAPP="923001234567";
let cart=JSON.parse(localStorage.getItem("cart")||"[]");

const products=[];
for(let i=1;i<=50;i++){
products.push({
id:i,
name:"Winter Product "+i,
price:1500+ i*10,
img:"https://picsum.photos/seed/winter"+i+"/400/400"
});
}

const box=document.getElementById("products");
products.forEach(p=>{
box.innerHTML+=`
<div class="card">
<img src="${p.img}">
<h4>${p.name}</h4>
<div class="price">PKR ${p.price}</div>
<button onclick="addToCart(${p.id})">Add to Cart</button>
</div>`;
});

function addToCart(id){
const p=products.find(x=>x.id===id);
cart.push(p);
save();alert("Added");
}

function toggleCart(){
document.getElementById("cartBox").style.display=
document.getElementById("cartBox").style.display=="block"?"none":"block";
renderCart();
}

function renderCart(){
let html="",sum=0;
cart.forEach((p,i)=>{
sum+=p.price;
html+=`<div class="cartItem">${p.name}<span>PKR ${p.price}</span></div>`;
});
document.getElementById("cartItems").innerHTML=html;
document.getElementById("total").innerText="Total: PKR "+sum;
}

function checkout(){
if(!cart.length){alert("Cart empty");return}
document.getElementById("paymentBox").style.display="block";
}

function closePayment(){
document.getElementById("paymentBox").style.display="none";
}

function confirmPayment(){
const tx=document.getElementById("txid").value;
if(!tx){alert("Enter Transaction ID");return}
let method=document.getElementById("payMethod").value;
let msg="NEW ORDER%0A";
cart.forEach(p=>msg+=`${p.name} - PKR ${p.price}%0A`);
msg+=`Payment: ${method}%0ATXID: ${tx}`;
window.open(`https://wa.me/${WHATSAPP}?text=${msg}`,"_blank");
cart=[];save();closePayment();toggleCart();
}

function save(){
localStorage.setItem("cart",JSON.stringify(cart));
}
</script>

</body>
</html>
