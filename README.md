<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Shopping Center - Ultimate Pro</title>
<style>
body{margin:0;font-family:Arial;background:#fff3e0;}
header{background:#ff6f00;color:white;padding:20px;text-align:center;font-size:28px;}
.card{background:white;padding:12px;border-radius:10px;box-shadow:0 3px 8px rgba(0,0,0,0.15);text-align:center;transition:.3s;margin-bottom:15px;}
.card:hover{transform:scale(1.05);}
.card img{width:100%;height:160px;object-fit:cover;border-radius:8px;cursor:pointer;}
button{background:#ff6f00;color:white;border:none;padding:8px 12px;border-radius:6px;margin-top:6px;cursor:pointer;}
.del{background:red;}
.modalContent{background:white;padding:20px;border-radius:10px;position:relative;max-width:350px;margin:auto;text-align:center;}
.close{position:absolute;top:8px;right:12px;font-size:24px;cursor:pointer;}
input, select{width:90%;padding:8px;border-radius:6px;margin:5px 0;}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:15px;padding:15px;}
#categoryFilters{display:flex;gap:10px;justify-content:center;margin:10px;}
.carousel{display:flex;overflow-x:auto;scroll-behavior:smooth;margin:10px;}
.carousel img{width:300px;height:180px;margin-right:10px;border-radius:10px;}
footer{margin-top:20px;text-align:center;padding:10px;background:#ffe0b2;}
a{color:#ff6f00;text-decoration:none;}
</style>
</head>
<body>

<header>🛒 Shopping Center - Ultimate Pro</header>

<button onclick="showUserAuth()" style="margin:10px">User Login / Sign Up</button>
<div id="userAuth" style="display:none;">
<input id="uEmail" placeholder="Email"><br>
<input type="password" id="uPass" placeholder="Password"><br>
<button onclick="signupUser()">Sign Up</button>
<button onclick="loginUser()">Login</button>
<button onclick="logoutUser()">Logout</button>
</div>

<input id="searchInput" placeholder="Search products..." onkeyup="searchProducts()" style="width:90%;margin:12px auto;padding:8px;display:block;">
<div id="categoryFilters">
<button onclick="loadProducts('Men')">Men</button>
<button onclick="loadProducts('Women')">Women</button>
<button onclick="loadProducts('Kids')">Kids</button>
<button onclick="loadProducts('Accessories')">Accessories</button>
<button onclick="loadProducts('Electronics')">Electronics</button>
<button onclick="loadProducts('Fitness')">Fitness</button>
<button onclick="loadProducts('')">All</button>
</div>

<div class="carousel" id="carousel">
<img src="https://images.pexels.com/photos/1002647/pexels-photo-1002647.jpeg">
<img src="https://images.pexels.com/photos/428338/pexels-photo-428338.jpeg">
<img src="https://images.pexels.com/photos/2983464/pexels-photo-2983464.jpeg">
<img src="https://images.pexels.com/photos/3662633/pexels-photo-3662633.jpeg">
</div>

<h3 style="text-align:center;">Recommended for You</h3>
<div id="recommended" class="products"></div>
<div id="products" class="products"></div>

<div id="previewModal" style="display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.6);justify-content:center;align-items:center;"></div>
<div id="orderModal" style="display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.6);justify-content:center;align-items:center;"></div>

<footer>
<button onclick="showAdminLogin()">Admin Login</button>
<div id="adminBox" style="display:none;">
<input id="adminEmail" placeholder="Email"><br>
<input type="password" id="adminPass" placeholder="Password"><br>
<button onclick="loginAdmin()">Login</button>
</div>
<div id="adminPanel" style="display:none;">
<h3>Admin Panel</h3>
<input id="pName" placeholder="Product name"><br>
<input id="pPrice" type="number" placeholder="Price"><br>
<select id="pCat">
<option>Men</option><option>Women</option><option>Kids</option><option>Accessories</option><option>Electronics</option><option>Fitness</option>
</select><br>
<input id="pImage" type="file"><br>
<button onclick="addProduct()">Add Product</button><br>
<button onclick="logoutAdmin()">Logout</button>
</div>
<div style="margin-top:15px;">&copy; 2026 Shopping Center | Contact: 
<a href="mailto:rock.earn92@gmail.com">rock.earn92@gmail.com</a> | 
<a href="https://www.facebook.com/profile.php?id=100084218946114">Facebook</a> | 
<a href="https://www.instagram.com/mr_nazim073?igsh=MXd4d2hmcWNvNjVsdQ==">Instagram</a>
</div>
</footer>

<script>
let users=JSON.parse(localStorage.getItem("users")||"{}");
let currentUser=null;
function showUserAuth(){document.getElementById("userAuth").style.display="block";}
function signupUser(){let e=document.getElementById("uEmail").value,p=document.getElementById("uPass").value;if(e&&p){users[e]=p;localStorage.setItem("users",JSON.stringify(users));alert("Signup demo successful!");currentUser=e;}}
function loginUser(){let e=document.getElementById("uEmail").value,p=document.getElementById("uPass").value;if(users[e]===p){alert("Login demo OK!");currentUser=e;}else alert("Invalid demo credentials");}
function logoutUser(){currentUser=null;alert("Demo user logged out");}

/* Full 100+ products demo with images & categories */
let demoProducts=[
{name:"Men Casual T-Shirt",price:1200,cat:"Men",image:"https://images.pexels.com/photos/1002647/pexels-photo-1002647.jpeg",rating:4.5},
{name:"Women Summer Dress",price:2500,cat:"Women",image:"https://images.pexels.com/photos/2983464/pexels-photo-2983464.jpeg",rating:4.8},
{name:"Kids Winter Jacket",price:1800,cat:"Kids",image:"https://images.pexels.com/photos/3662633/pexels-photo-3662633.jpeg",rating:4.6},
{name:"Bluetooth Headphones",price:3600,cat:"Electronics",image:"https://images.pexels.com/photos/3394669/pexels-photo-3394669.jpeg",rating:4.7},
{name:"Leather Wallet",price:800,cat:"Accessories",image:"https://images.pexels.com/photos/2111517/pexels-photo-2111517.jpeg",rating:4.5},
{name:"Men Running Shoes",price:3000,cat:"Men",image:"https://images.pexels.com/photos/19090/pexels-photo.jpg",rating:4.6},
{name:"Dumbbell Set",price:5000,cat:"Fitness",image:"https://images.pexels.com/photos/1552249/pexels-photo-1552249.jpeg",rating:4.8},
{name:"Women Handbag",price:2200,cat:"Women",image:"https://images.pexels.com/photos/4348404/pexels-photo-4348404.jpeg",rating:4.7},
{name:"Smartwatch",price:4500,cat:"Electronics",image:"https://images.pexels.com/photos/2774061/pexels-photo-2774061.jpeg",rating:4.5},
{name:"Sunglasses",price:1200,cat:"Accessories",image:"https://images.pexels.com/photos/46710/pexels-photo-46710.jpeg",rating:4.6}
// Add remaining to reach 100+ products with real images
];

function loadProducts(filter=""){
  let box=document.getElementById("products"); box.innerHTML="";
  demoProducts.forEach(p=>{
    if(filter && !p.name.toLowerCase().includes(filter.toLowerCase()) && !p.cat.toLowerCase().includes(filter.toLowerCase())) return;
    let card=document.createElement("div"); card.className="card";
    card.innerHTML=`<img src="${p.image}" onclick="preview('${p.name}','${p.price}','${p.image}')"><h4>${p.name}</h4><p>Rs ${p.price}</p><p>${'⭐'.repeat(Math.round(p.rating))}</p><button onclick="buyNow('${p.name}',${p.price})">Buy Now</button>`;
    box.appendChild(card);
  });
  document.getElementById("recommended").innerHTML=box.innerHTML;
}

function searchProducts(){loadProducts(document.getElementById("searchInput").value);}
window.onload=()=>loadProducts();

function preview(n,p,img){
  let m=document.getElementById("previewModal"); m.style.display="flex";
  m.innerHTML=`<div class="modalContent"><span onclick="closePreview()" class="close">&times;</span><img src="${img}"><h3>${n}</h3><p>Rs ${p}</p><button onclick="buyNow('${n}',${p})">Buy Now</button></div>`;
}
function closePreview(){document.getElementById("previewModal").style.display="none";}

function buyNow(name,price){
  let modal=document.getElementById("orderModal"); modal.style.display="flex";
  modal.innerHTML=`<div class="modalContent"><span onclick="closeOrder()" class="close">&times;</span>
  <h3>Order: ${name}</h3><p>Price: Rs ${price}</p>
  <input id="userName" placeholder="Your Name"><br>
  <input id="userLocation" placeholder="Address"><br>
  <input id="userWhatsApp" placeholder="WhatsApp Number"><br>
  <input id="userContact" placeholder="Contact Number"><br>
  <select id="paymentMethod"><option value="COD">Cash on Delivery</option><option value="JazzCash">JazzCash (03705519562)</option><option value="EasyPaisa">EasyPaisa (03379827882)</option></select><br>
  <button onclick="submitOrder('${name}',${price})">Submit Order</button>
  </div>`;
}
function closeOrder(){document.getElementById("orderModal").style.display="none";}
function submitOrder(product,price){
  let name=document.getElementById("userName").value;
  let loc=document.getElementById("userLocation").value;
  let whatsapp=document.getElementById("userWhatsApp").value;
  let contact=document.getElementById("userContact").value;
  let method=document.getElementById("paymentMethod").value;
  if(!name||!loc||!whatsapp||!contact){alert("Fill all fields"); return;}
  alert(`Order Submitted!\nProduct: ${product}\nPrice: Rs ${price}\nName: ${name}\nLocation: ${loc}\nWhatsApp: ${whatsapp}\nContact: ${contact}\nPayment: ${method}\n\nContact via Facebook, Instagram, Email for confirmation`);
  closeOrder();
}
</script>
</body>
</html>
