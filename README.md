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
.admin-panel{background:#fff;padding:15px;border-radius:12px;box-shadow:0 4px 15px rgba(0,0,0,0.2);margin-bottom:20px;display:none}
.admin-panel h3{margin-top:0;color:#333}
.login-panel{background:#fff;padding:15px;border-radius:12px;box-shadow:0 4px 15px rgba(0,0,0,0.2);margin-bottom:20px;text-align:center}
.login-panel input{margin:5px;width:200px}
.login-panel button{width:220px}
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

<!-- ADMIN LOGIN -->
<div class="login-panel" id="loginPanel">
<h3>Admin Login</h3>
<input type="text" id="adminUser" placeholder="Username"><br>
<input type="password" id="adminPass" placeholder="Password"><br>
<button onclick="loginAdmin()">Login</button>
</div>

<!-- ADMIN PANEL -->
<div class="admin-panel" id="adminPanel">
<h3>Admin Panel (Owner Only)</h3>
<input type="text" id="adminName" placeholder="Product Name">
<input type="number" id="adminPrice" placeholder="Price">
<input type="text" id="adminDesc" placeholder="Description">
<select id="adminCat">
<option value="Men">Men</option>
<option value="Women">Women</option>
<option value="Accessories">Accessories</option>
<option value="Electronics">Electronics</option>
<option value="Fitness">Fitness</option>
</select>
<input type="file" id="adminImg" accept="image/*">
<button onclick="addProduct()">Add / Update Product</button>
<button onclick="logoutAdmin()">Logout</button>
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
// Admin credentials (for demo)
const ADMIN_USERNAME="admin";
const ADMIN_PASSWORD="123456";

// Load products from LocalStorage or default demo list
let products = JSON.parse(localStorage.getItem("products")) || [
{name:"Men Casual Watch",price:2999,img:"https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=300&h=300&fit=crop",desc:"Stylish casual watch for men.",cat:"Men"},
{name:"Wireless Bluetooth Headphones",price:4499,img:"https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=300&h=300&fit=crop",desc:"Noise reduction, long battery life.",cat:"Electronics"},
{name:"Women Leather Handbag",price:3899,img:"https://images.unsplash.com/photo-1584917865442-de89df76afd3?w=300&h=300&fit=crop",desc:"Elegant handbag for daily use.",cat:"Women"}
];

let cart = [];

// Render products
function renderProducts(){
 let searchVal=search.value.toLowerCase();
 let catVal=filterCat.value;
 let filtered=products.filter(p=>p.name.toLowerCase().includes(searchVal)&&(catVal==""||p.cat==catVal));
 document.getElementById("products").innerHTML = filtered.map((p,i)=>`
 <div class="card">
  <img src="${p.img}" loading="lazy">
  <h4>${p.name}</h4>
  <p>${p.desc}</p>
  <div class="price">Rs. ${p.price}</div>
  <button onclick="addCart(${i})">Add to Cart</button>
  ${document.getElementById("adminPanel").style.display==="block"?`<button onclick="editProduct(${i})">Edit</button><button onclick="deleteProduct(${i})">Delete</button>`:""}
 </div>`).join("");
}

// Cart functions
function addCart(i){cart.push(products[i]);renderCart();}
function renderCart(){document.getElementById("cart").innerHTML=cart.map(c=>`${c.name} - Rs.${c.price}`).join("<br>");}
function checkout(){
 if(cart.length==0){alert("Cart is empty"); return;}
 let msg=cart.map(c=>c.name+" Rs."+c.price).join("%0A");
 let paymentMethod=document.getElementById("payment").value;
 msg+="%0A%0APayment Method: "+paymentMethod;
 window.open("https://wa.me/923000000000?text=Order%0A"+msg);
 cart=[];
 renderCart();
}

// Admin Panel functions
function loginAdmin(){
 let u=document.getElementById("adminUser").value;
 let p=document.getElementById("adminPass").value;
 if(u===ADMIN_USERNAME && p===ADMIN_PASSWORD){
  document.getElementById("adminPanel").style.display="block";
  document.getElementById("loginPanel").style.display="none";
  renderProducts();
 } else {alert("Invalid credentials");}
}
function logoutAdmin(){
 document.getElementById("adminPanel").style.display="none";
 document.getElementById("loginPanel").style.display="block";
 renderProducts();
}

function addProduct(){
 let name=document.getElementById("adminName").value;
 let price=document.getElementById("adminPrice").value;
 let desc=document.getElementById("adminDesc").value;
 let cat=document.getElementById("adminCat").value;
 let imgInput=document.getElementById("adminImg");
 if(name==""||price==""||desc==""||!imgInput.files[0]){alert("Fill all fields and choose image"); return;}
 let reader=new FileReader();
 reader.onload=function(e){
  let img=e.target.result;
  products.push({name,price,img,desc,cat});
  localStorage.setItem("products",JSON.stringify(products));
  renderProducts();
  document.getElementById("adminName").value="";
  document.getElementById("adminPrice").value="";
  document.getElementById("adminDesc").value="";
  imgInput.value="";
 };
 reader.readAsDataURL(imgInput.files[0]);
}

function editProduct(i){
 let p=products[i];
 let newName=prompt("Edit Name:",p.name); if(!newName)return;
 let newPrice=prompt("Edit Price:",p.price); if(!newPrice)return;
 let newDesc=prompt("Edit Description:",p.desc); if(!newDesc)return;
 let newCat=prompt("Edit Category (Men/Women/Accessories/Electronics/Fitness):",p.cat); if(!newCat)return;
 products[i]={...p,name:newName,price:newPrice,desc:newDesc,cat:newCat};
 localStorage.setItem("products",JSON.stringify(products));
 renderProducts();
}

function deleteProduct(i){
 if(confirm("Are you sure you want to delete this product?")){
  products.splice(i,1);
  localStorage.setItem("products",JSON.stringify(products));
  renderProducts();
 }
}

renderProducts();
renderCart();
</script>

</body>
</html>
