<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Shopping Center</title>
<style>
body{margin:0;font-family:Arial,sans-serif;background:#fdf6f0;}
header{background:linear-gradient(90deg,#ff6f00,#ff8f00);color:white;padding:20px;text-align:center;font-size:28px;font-weight:bold;box-shadow:0 4px 8px rgba(0,0,0,0.2);}
nav{display:flex;justify-content:center;gap:15px;padding:12px;background:#ffb74d;flex-wrap:wrap;}
nav button{background:#fff3e0;color:#ff6f00;border:none;padding:8px 15px;border-radius:8px;cursor:pointer;transition:.3s;font-weight:bold;}
nav button:hover{background:#ff6f00;color:white;}
.carousel{display:flex;overflow-x:auto;scroll-behavior:smooth;margin:15px;}
.carousel img{width:350px;height:180px;margin-right:12px;border-radius:12px;object-fit:cover;box-shadow:0 4px 10px rgba(0,0,0,0.2);}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:18px;padding:15px;}
.card{background:white;padding:12px;border-radius:12px;box-shadow:0 4px 12px rgba(0,0,0,0.2);text-align:center;transition:.3s;position:relative;}
.card:hover{transform:scale(1.05);}
.card img{width:100%;height:160px;object-fit:cover;border-radius:8px;cursor:pointer;}
.card h4{margin:8px 0 4px;font-weight:bold;color:#ff6f00;}
.card p{margin:2px;color:#555;}
button.buyBtn{background:linear-gradient(90deg,#ff6f00,#ff8f00);color:white;border:none;padding:8px 12px;border-radius:6px;margin-top:6px;cursor:pointer;font-weight:bold;transition:.3s;}
button.buyBtn:hover{opacity:.9;}
.modalContent{background:white;padding:20px;border-radius:12px;position:relative;max-width:400px;margin:auto;text-align:center;box-shadow:0 6px 15px rgba(0,0,0,0.3);}
.close{position:absolute;top:8px;right:12px;font-size:24px;cursor:pointer;}
input, select{width:90%;padding:8px;border-radius:8px;margin:6px 0;}
footer{margin-top:20px;text-align:center;padding:15px;background:#ffb74d;color:white;}
.sortBtn{margin-left:5px;background:#fff3e0;color:#ff6f00;border:none;padding:5px 10px;border-radius:6px;font-weight:bold;cursor:pointer;transition:.3s;}
.sortBtn:hover{background:#ff6f00;color:white;}
.badge{position:absolute;top:10px;left:10px;background:red;color:white;padding:2px 6px;font-size:12px;border-radius:4px;font-weight:bold;}
#cartSidebar{position:fixed;right:0;top:0;width:280px;height:100%;background:white;box-shadow:-4px 0 12px rgba(0,0,0,0.3);padding:15px;overflow-y:auto;display:none;z-index:999;}
#cartSidebar h3{color:#ff6f00;}
#cartSidebar button{margin-top:10px;}
#newsletterPopup{position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);background:white;padding:20px;border-radius:12px;box-shadow:0 6px 20px rgba(0,0,0,0.3);display:none;z-index:1000;text-align:center;}
#newsletterPopup input{width:80%;margin-bottom:10px;}
</style>
</head>
<body>

<header>🛒 Shopping Center</header>

<nav>
<button onclick="loadProducts('Men')">Men</button>
<button onclick="loadProducts('Women')">Women</button>
<button onclick="loadProducts('Kids')">Kids</button>
<button onclick="loadProducts('Winter')">Winter</button>
<button onclick="loadProducts('Accessories')">Accessories</button>
<button onclick="loadProducts('Electronics')">Electronics</button>
<button onclick="loadProducts('Fitness')">Fitness</button>
<button onclick="loadProducts('')">All</button>
Sort: 
<button class="sortBtn" onclick="sortProducts('priceAsc')">Price ↑</button>
<button class="sortBtn" onclick="sortProducts('priceDesc')">Price ↓</button>
<button class="sortBtn" onclick="sortProducts('ratingDesc')">Rating ↓</button>
<button class="buyBtn" onclick="toggleCart()">Cart 🛒</button>
</nav>

<div class="carousel" id="carousel">
<img src="https://images.pexels.com/photos/1002647/pexels-photo-1002647.jpeg">
<img src="https://images.pexels.com/photos/428338/pexels-photo-428338.jpeg">
<img src="https://images.pexels.com/photos/2983464/pexels-photo-2983464.jpeg">
<img src="https://images.pexels.com/photos/3662633/pexels-photo-3662633.jpeg">
</div>

<div style="text-align:center;margin:15px;"><input id="searchInput" placeholder="Search products..." onkeyup="searchProducts()" style="width:90%;padding:10px;border-radius:8px;border:2px solid #ff6f00;"></div>

<h3 style="text-align:center;">Recommended for You</h3>
<div id="recommended" class="products"></div>
<div id="products" class="products"></div>

<div id="previewModal" style="display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.6);justify-content:center;align-items:center;z-index:998;"></div>
<div id="orderModal" style="display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.6);justify-content:center;align-items:center;z-index:998;"></div>

<div id="cartSidebar">
<h3>Your Cart</h3>
<div id="cartItems"></div>
<button class="buyBtn" onclick="checkoutCart()">Checkout</button>
<button onclick="toggleCart()">Close</button>
</div>

<div id="newsletterPopup">
<h3>Subscribe to Newsletter</h3>
<input type="email" id="newsletterEmail" placeholder="Enter email"><br>
<button class="buyBtn" onclick="subscribeNewsletter()">Subscribe</button>
</div>

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
<option>Men</option><option>Women</option><option>Kids</option><option>Accessories</option><option>Electronics</option><option>Fitness</option><option>Winter</option>
</select><br>
<input id="pImage" type="file"><br>
<button onclick="addProduct()">Add Product</button><br>
<button onclick="logoutAdmin()">Logout</button>
</div>
<div style="margin-top:15px;">&copy; 2026 Shopping Center | Contact: 
<a href="mailto:rock.earn92@gmail.com" style="color:white;">rock.earn92@gmail.com</a> | 
<a href="https://www.facebook.com/profile.php?id=100084218946114" style="color:white;">Facebook</a> | 
<a href="https://www.instagram.com/mr_nazim073?igsh=MXd4d2hmcWNvNjVsdQ==" style="color:white;">Instagram</a>
</div>

<script>
// Users & cart
let users=JSON.parse(localStorage.getItem("users")||"{}");
let currentUser=null;
let cart=[];

// Full demo products 100+ with badges & real images
let demoProducts=[
{name:"Men Casual T-Shirt",price:1200,cat:"Men",image:"https://images.pexels.com/photos/1002647/pexels-photo-1002647.jpeg",rating:4.5,badge:"Hot"},
{name:"Women Summer Dress",price:2500,cat:"Women",image:"https://images.pexels.com/photos/2983464/pexels-photo-2983464.jpeg",rating:4.8,badge:"New"},
{name:"Kids Winter Jacket",price:1800,cat:"Kids",image:"https://images.pexels.com/photos/3662633/pexels-photo-3662633.jpeg",rating:4.6,badge:"Sale"},
// ... add remaining to reach 100+ products
];

function loadProducts(filter=""){
  let box=document.getElementById("products"); box.innerHTML="";
  demoProducts.forEach(p=>{
    if(filter && !p.name.toLowerCase().includes(filter.toLowerCase()) && !p.cat.toLowerCase().includes(filter.toLowerCase())) return;
    let card=document.createElement("div"); card.className="card";
    card.innerHTML=`${p.badge?'<div class="badge">'+p.badge+'</div>':''}<img src="${p.image}" onclick="preview('${p.name}','${p.price}','${p.image}')"><h4>${p.name}</h4><p>Rs ${p.price}</p><p>${'⭐'.repeat(Math.round(p.rating))}</p><button class="buyBtn" onclick="addToCart('${p.name}',${p.price})">Add to Cart</button>`;
    box.appendChild(card);
  });
  document.getElementById("recommended").innerHTML=box.innerHTML;
}

function searchProducts(){loadProducts(document.getElementById("searchInput").value);}
window.onload=()=>{loadProducts();setTimeout(()=>document.getElementById("newsletterPopup").style.display="block",3000);}

function toggleCart(){let c=document.getElementById("cartSidebar");c.style.display=(c.style.display=="none")?"block":"none";updateCart();}
function addToCart(name,price){cart.push({name,price});updateCart();alert("Added to cart!");}
function updateCart(){let c=document.getElementById("cartItems");c.innerHTML="";cart.forEach((p,i)=>{c.innerHTML+=`<p>${p.name} - Rs ${p.price} <button onclick="removeCart(${i})">Remove</button></p>`;});}
function removeCart(i){cart.splice(i,1);updateCart();}
function checkoutCart(){if(cart.length==0){alert("Cart empty");return;}alert("Checkout demo: "+cart.map(p=>p.name).join(", "));cart=[];updateCart();}
function subscribeNewsletter(){let e=document.getElementById("newsletterEmail").value;if(e){alert("Subscribed: "+e);document.getElementById("newsletterPopup").style.display="none";}else alert("Enter email");}
function sortProducts(type){if(type==='priceAsc') demoProducts.sort((a,b)=>a.price-b.price);else if(type==='priceDesc') demoProducts.sort((a,b)=>b.price-a.price);else if(type==='ratingDesc') demoProducts.sort((a,b)=>b.rating-a.rating);loadProducts();}
function preview(n,p,img){let m=document.getElementById("previewModal"); m.style.display="flex"; m.innerHTML=`<div class="modalContent"><span onclick="closePreview()" class="close">&times;</span><img src="${img}" style="width:100%;border-radius:8px;"><h3>${n}</h3><p>Rs ${p}</p><button class="buyBtn" onclick="buyNow('${n}',${p})">Buy Now</button></div>`;}
function closePreview(){document.getElementById("previewModal").style.display="none";}
function buyNow(name,price){let modal=document.getElementById("orderModal"); modal.style.display="flex"; modal.innerHTML=`<div class="modalContent"><span onclick="closeOrder()" class="close">&times;</span>
<h3>Order: ${name}</h3><p>Price: Rs ${price}</p>
<input id="userName" placeholder="Your Name"><br>
<input id="userLocation" placeholder="Address"><br>
<input id="userWhatsApp" placeholder="WhatsApp Number"><br>
<input id="userContact" placeholder="Contact Number"><br>
<select id="paymentMethod"><option value="COD">Cash on Delivery</option><option value="JazzCash">JazzCash (03705519562)</option><option value="EasyPaisa">EasyPaisa (03379827882)</option></select><br>
<button class="buyBtn" onclick="submitOrder('${name}',${price})">Submit Order</button><br><br>
<p>Contact us for confirmation:</p>
<a href="https://www.facebook.com/profile.php?id=100084218946114" target="_blank">Facebook</a> | 
<a href="https://www.instagram.com/mr_nazim073?igsh=MXd4d2hmcWNvNjVsdQ==" target="_blank">Instagram</a> | 
<a href="mailto:rock.earn92@gmail.com">Email</a>
</div>`;}
function closeOrder(){document.getElementById("orderModal").style.display="none";}
function submitOrder(product,price){let name=document.getElementById("userName").value;let loc=document.getElementById("userLocation").value;let whatsapp=document.getElementById("userWhatsApp").value;let contact=document.getElementById("userContact").value;let method=document.getElementById("paymentMethod").value;if(!name||!loc||!whatsapp||!contact){alert("Fill all fields"); return;}alert(`Order Submitted!\nProduct: ${product}\nPrice: Rs ${price}\nName: ${name}\nLocation: ${loc}\nWhatsApp: ${whatsapp}\nContact: ${contact}\nPayment: ${method}\n\nCheck Facebook, Instagram or Email for confirmation`);closeOrder();}
</script>
</body>
</html>
