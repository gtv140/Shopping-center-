<shop>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#f9f9f9;color:#222;padding-bottom:100px}
header{background:#111;color:#fff;padding:15px;text-align:center}
header input{margin-top:10px;padding:8px;width:90%;max-width:400px;border-radius:5px;border:none}
.categories{display:flex;justify-content:center;flex-wrap:wrap;gap:10px;margin:12px 0}
.categories button{background:#eee;border:none;padding:10px;border-radius:50px;cursor:pointer;font-size:14px;transition:all .3s}
.categories button:hover{background:#ddd}
.products{padding:20px;display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:16px}
.product{background:#fff;border-radius:10px;overflow:hidden;box-shadow:0 3px 10px rgba(0,0,0,.1);position:relative;transition:all .3s}
.product:hover{transform:translateY(-5px)}
.product img{width:100%;height:180px;object-fit:cover}
.info{padding:10px}
.info h3{margin:0;font-size:15px}
.price{font-weight:bold;margin:5px 0}
.buttons a{display:block;text-align:center;margin-top:6px;padding:6px;border-radius:6px;color:#fff;text-decoration:none;font-size:13px}
.insta{background:#e1306c}
.fb{background:#1877f2}
.mail{background:#000}
.badge{position:absolute;top:10px;left:10px;background:#f00;color:#fff;padding:4px 6px;font-size:12px;border-radius:4px}
.ads{margin:20px auto;padding:12px;background:#fffae5;border-radius:8px;text-align:center;font-weight:bold;color:#222;box-shadow:0 2px 8px rgba(0,0,0,.1)}
.recent{background:#fff;margin:20px;padding:15px;border-radius:10px}
.recent span{display:inline-block;background:#eee;padding:6px 10px;margin:4px;border-radius:20px;font-size:13px}
footer{background:#111;color:#aaa;text-align:center;padding:12px;font-size:13px}
.slider{width:100%;overflow:hidden;margin:15px 0;position:relative;height:220px;border-radius:10px}
.slide{width:100%;height:100%;position:absolute;top:0;left:100%;transition:all 0.5s ease;}
.slide.active{left:0;}
.bottom-bar{position:fixed;bottom:0;left:0;width:100%;background:#fff;display:flex;justify-content:space-around;align-items:center;padding:10px 0;box-shadow:0 -2px 8px rgba(0,0,0,.2);z-index:1000}
.bottom-bar button{background:#eee;border:none;padding:10px;border-radius:50%;font-size:20px;cursor:pointer;transition:all .3s;}
.bottom-bar button:hover{background:#ddd}
</style>
</head>
<body>

<header>
<h1>Shopping Center</h1>
<p>Clean • Premium • Smart Store</p>
<input type="text" id="search" placeholder="Search products...">
</header>

<div class="categories">
<button onclick="filterCategory('All')">🏷️ All</button>
<button onclick="filterCategory('Electronics')">📱 Electronics</button>
<button onclick="filterCategory('Audio')">🎧 Audio</button>
<button onclick="filterCategory('Accessories')">⌚ Accessories</button>
<button onclick="filterCategory('Fashion')">👗 Fashion</button>
<button onclick="filterCategory('Shoes')">👟 Shoes</button>
<button onclick="filterCategory('Bags')">👜 Bags</button>
<button onclick="filterCategory('Watches')">⌚ Watches</button>
<button onclick="filterCategory('Gadgets')">🔌 Gadgets</button>
</div>

<div class="slider" id="slider">
<img src="https://images.unsplash.com/photo-1512499617640-c2f99912f7fa?auto=format&fit=crop&w=800&q=80" class="slide active">
<img src="https://images.unsplash.com/photo-1606813902854-25e01744674c?auto=format&fit=crop&w=800&q=80" class="slide">
<img src="https://images.unsplash.com/photo-1600180758895-9a3d1f07b09d?auto=format&fit=crop&w=800&q=80" class="slide">
</div>

<div class="ads" id="ads">🔥 Hot Deal: Smart Phone PKR 54,999 - Limited Time!</div>

<section class="products" id="productList">

<!-- Example Product 1 -->
<div class="product" data-name="Smart Phone" data-category="Electronics">
<div class="badge">🔥 Trending</div>
<img src="https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?auto=format&fit=crop&w=400&q=80" alt="Smart Phone">
<div class="info">
<h3>Smart Phone</h3>
<div class="price">PKR 54,999</div>
<div class="buttons">
<a class="insta" href="https://www.instagram.com/shoppingcenter664?igsh=MW0zZTZoOTB4aXc1Mg==" target="_blank">Instagram</a>
<a class="fb" href="https://www.facebook.com/profile.php?id=61581475052443" target="_blank">Facebook</a>
<a class="mail" href="mailto:rock.earn92@gmail.com">Gmail</a>
</div>
<button onclick="addToCart('Smart Phone')">Add to Cart</button>
</div>
</div>

<!-- Example Product 2 -->
<div class="product" data-name="Headphones" data-category="Audio">
<img src="https://images.unsplash.com/photo-1519985176271-adb1088fa94c?auto=format&fit=crop&w=400&q=80" alt="Headphones">
<div class="info">
<h3>Headphones</h3>
<div class="price">PKR 1,799</div>
<div class="buttons">
<a class="insta" href="https://www.instagram.com/shoppingcenter664?igsh=MW0zZTZoOTB4aXc1Mg==" target="_blank">Instagram</a>
<a class="fb" href="https://www.facebook.com/profile.php?id=61581475052443" target="_blank">Facebook</a>
<a class="mail" href="mailto:rock.earn92@gmail.com">Gmail</a>
</div>
<button onclick="addToCart('Headphones')">Add to Cart</button>
</div>
</div>

<!-- Example Product 3 -->
<div class="product" data-name="Smart Watch" data-category="Accessories">
<img src="https://images.unsplash.com/photo-1516574187841-cb9cc2ca948b?auto=format&fit=crop&w=400&q=80" alt="Smart Watch">
<div class="info">
<h3>Smart Watch</h3>
<div class="price">PKR 12,999</div>
<div class="buttons">
<a class="insta" href="https://www.instagram.com/shoppingcenter664?igsh=MW0zZTZoOTB4aXc1Mg==" target="_blank">Instagram</a>
<a class="fb" href="https://www.facebook.com/profile.php?id=61581475052443" target="_blank">Facebook</a>
<a class="mail" href="mailto:rock.earn92@gmail.com">Gmail</a>
</div>
<button onclick="addToCart('Smart Watch')">Add to Cart</button>
</div>
</div>

<!-- Repeat other products similarly for Fashion, Shoes, Bags, Watches, Gadgets -->

</section>

<div class="recent">
<strong>Recently Viewed:</strong><br>
<div id="recentItems"></div>
</div>

<footer>© 2026 Shopping Center</footer>

<div id="cartBtn">🛒 Cart</div>

<div class="bottom-bar">
<button onclick="window.scrollTo({top:0,behavior:'smooth'})">🏠</button>
<button onclick="document.getElementById('cartBtn').click()">🛒</button>
<button onclick="window.scrollTo({top:200,behavior:'smooth'})">🔖</button>
<button onclick="alert('Trending / Sale')">⭐</button>
<button onclick="alert('Order Now / Profile')">👤</button>
</div>

<script>
// SLIDER
let slides = document.querySelectorAll('.slide');
let current = 0;
setInterval(()=>{
slides[current].classList.remove('active');
current = (current + 1) % slides.length;
slides[current].classList.add('active');
}, 4000);

// CART
let cart = JSON.parse(localStorage.getItem("cart")) || [];
function addToCart(name){
cart.push(name);
localStorage.setItem("cart", JSON.stringify(cart));
alert(name + " added to cart");
addRecent(name);
}

// SEARCH
document.getElementById("search").addEventListener("keyup", function(){
let val = this.value.toLowerCase();
document.querySelectorAll(".product").forEach(p=>{
p.style.display = p.dataset.name.toLowerCase().includes(val) ? "block" : "none";
});
});

// CATEGORY FILTER
function filterCategory(cat){
document.querySelectorAll(".product").forEach(p=>{
p.style.display = (cat=="All" || p.dataset.category==cat) ? "block" : "none";
});
}

// RECENT VIEWED
function addRecent(name){
let recent = JSON.parse(localStorage.getItem("recent")) || [];
if(!recent.includes(name)){
recent.unshift(name);
if(recent.length>5) recent.pop();
localStorage.setItem("recent", JSON.stringify(recent));
}
showRecent();
}
function showRecent(){
let recent = JSON.parse(localStorage.getItem("recent")) || [];
document.getElementById("recentItems").innerHTML = recent.map(i=>`<span>${i}</span>`).join("");
}
showRecent();

// CART VIEW
document.getElementById("cartBtn").onclick = function(){
alert("Cart Items:\n" + (cart.length ? cart.join(", ") : "Cart empty"));
}

// ADS ROTATOR
let ads = [
"🔥 Hot Deal: Smart Phone PKR 54,999",
"💥 Sale: Headphones PKR 1,799",
"⭐ Trending: Smart Watch PKR 12,999",
"🎧 Gadgets: Wireless Charger PKR 999",
"👜 Fashion Bags PKR 2,499"
];
let adIndex = 0;
setInterval(()=>{
document.getElementById("ads").innerText = ads[adIndex];
adIndex = (adIndex + 1) % ads.length;
}, 6000);
</script>

</body>
</html>
