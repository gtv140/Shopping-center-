<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>SHOPPING CENTER - Trending</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body{margin:0;font-family:Arial,sans-serif;background:#111;color:#fff}
header{background:#000;padding:20px;text-align:center;box-shadow:0 2px 15px rgba(255,255,255,0.1)}
header h1{color:#0ff;font-size:36px;margin:0;text-shadow:0 0 5px #0ff}
header p{color:#aaa;margin-top:5px}
.search-bar{margin:15px auto;text-align:center}
.search-bar input{padding:12px;width:80%;border-radius:12px;border:1px solid #0ff;background:#111;color:#fff;outline:none}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:20px;padding:20px}
.card{background:#1a1a1a;border-radius:12px;padding:15px;text-align:center;box-shadow:0 2px 15px rgba(0,255,255,0.1);transition:0.3s;position:relative}
.card:hover{transform:scale(1.05);box-shadow:0 0 20px #0ff}
.card img{width:100%;height:220px;object-fit:cover;border-radius:10px}
.price{color:#0ff;font-weight:bold;font-size:18px;margin:10px 0}
.badge{position:absolute;top:10px;left:10px;background:#e76f51;color:#fff;padding:5px 10px;border-radius:6px;font-size:12px;text-transform:uppercase; font-weight:bold;}
.btns button, .btns a{display:block;margin:5px 0;padding:10px;border-radius:8px;text-decoration:none;color:#fff;font-weight:bold;cursor:pointer;border:none}
.btn-add{background:#0ff;color:#000}
.btn-wish{background:#e76f51}
.btns a{background:#333;text-align:center}
.about{background:#222;margin:20px;padding:20px;border-radius:12px;box-shadow:0 2px 15px rgba(0,255,255,0.1)}
.bottom-bar{position:fixed;bottom:0;left:0;width:100%;background:#000;display:flex;justify-content:flex-end;align-items:center;padding:10px 20px;box-shadow:0 -2px 15px rgba(0,255,255,0.1);z-index:1000}
.menu-dropdown{position:relative;display:inline-block;}
.menu-btn{background:#0ff;color:#000;padding:10px 15px;border:none;border-radius:8px;cursor:pointer;font-weight:bold;}
.menu-content{display:none;position:absolute;bottom:50px;right:0;background:#111;min-width:200px;box-shadow:0 2px 15px rgba(0,255,255,0.3);border-radius:10px;z-index:1001}
.menu-content a{color:#0ff;padding:12px;display:block;text-decoration:none;font-weight:bold;}
.menu-content a:hover{background:#222}
.show{display:block;}
.ads-bar{background:#0ff;color:#000;text-align:center;padding:12px;margin:20px;border-radius:10px;box-shadow:0 2px 15px rgba(255,255,255,0.1);font-weight:bold;font-size:16px;}
</style>
</head>
<body>

<header>
<h1>SHOPPING CENTER</h1>
<p>Top Trending Items – Premium Online Shop</p>
<div class="search-bar">
<input type="text" id="searchInput" placeholder="Search products...">
</div>
</header>

<div class="ads-bar" id="adsBarTop">🔥 20% OFF on Trending Items! 🔥</div>

<section class="products" id="productContainer">

<!-- Product 1 -->
<div class="card">
<div class="badge">New</div>
<img src="images/product1.jpg" alt="Product 1">
<h3>Wireless Earbuds</h3>
<p class="price">Rs 2,499</p>
<div class="btns">
<button class="btn-add" onclick="addToCart('Wireless Earbuds',2499)">Add to Cart</button>
<button class="btn-wish" onclick="addToWish('Wireless Earbuds')">❤ Wishlist</button>
<a href="mailto:rock.earn92@gmail.com?subject=Order Wireless Earbuds&body=I want this">Gmail</a>
<a href="https://instagram.com/shoppingcenter664" target="_blank">Instagram</a>
<a href="https://m.me/61581475052443" target="_blank">Facebook</a>
</div>
</div>

<!-- Product 2 -->
<div class="card">
<div class="badge">Hot</div>
<img src="images/product2.jpg" alt="Product 2">
<h3>Smart LED Lamp</h3>
<p class="price">Rs 1,999</p>
<div class="btns">
<button class="btn-add" onclick="addToCart('Smart LED Lamp',1999)">Add to Cart</button>
<button class="btn-wish" onclick="addToWish('Smart LED Lamp')">❤ Wishlist</button>
<a href="mailto:rock.earn92@gmail.com?subject=Order Smart LED Lamp&body=I want this">Gmail</a>
<a href="https://instagram.com/shoppingcenter664" target="_blank">Instagram</a>
<a href="https://m.me/61581475052443" target="_blank">Facebook</a>
</div>
</div>

<!-- Product 3 -->
<div class="card">
<div class="badge">Trending</div>
<img src="images/product3.jpg" alt="Product 3">
<h3>Portable Power Bank</h3>
<p class="price">Rs 1,299</p>
<div class="btns">
<button class="btn-add" onclick="addToCart('Portable Power Bank',1299)">Add to Cart</button>
<button class="btn-wish" onclick="addToWish('Portable Power Bank')">❤ Wishlist</button>
<a href="mailto:rock.earn92@gmail.com?subject=Order Portable Power Bank&body=I want this">Gmail</a>
<a href="https://instagram.com/shoppingcenter664" target="_blank">Instagram</a>
<a href="https://m.me/61581475052443" target="_blank">Facebook</a>
</div>
</div>

<!-- Repeat similar structure up to 30 products, change filenames to product4.jpg, product5.jpg ... -->

</section>

<div class="ads-bar" id="adsBarBottom">🔥 Buy 1 Get 1 Free on Top Items! 🔥</div>

<div class="about">
<h2>About SHOPPING CENTER</h2>
<p>Welcome to SHOPPING CENTER – your destination for top trending products. Browse, add to cart, wishlist your favorites, and enjoy a professional premium shopping experience. Live discounts and rotating ads keep shopping exciting!</p>
</div>

<div class="bottom-bar">
<div class="menu-dropdown">
<button class="menu-btn" onclick="toggleMenu()">Menu ☰</button>
<div class="menu-content" id="menuContent">
<a href="#" onclick="scrollToSearch()">🔍 Search</a>
<a href="#" onclick="toggleWishlist()">❤ Wishlist</a>
<a href="#" onclick="toggleCart()">🛒 Cart</a>
<a href="https://instagram.com/shoppingcenter664" target="_blank">📸 Instagram</a>
<a href="https://m.me/61581475052443" target="_blank">📘 Facebook</a>
<a href="mailto:rock.earn92@gmail.com">✉️ Gmail</a>
</div>
</div>
</div>

<footer>
<p style="text-align:center;padding:10px;color:#aaa;">© 2026 SHOPPING CENTER</p>
</footer>

<script>
// Cart & Wishlist
let cart = JSON.parse(localStorage.getItem('cart')) || [];
let wishlist = JSON.parse(localStorage.getItem('wishlist')) || [];

function addToCart(name, price){
    let item = cart.find(i=>i.name===name);
    if(item){item.qty +=1;} else {cart.push({name:name, price:price, qty:1});}
    localStorage.setItem('cart', JSON.stringify(cart));
    updateCart();
}
function updateCart(){localStorage.setItem('cart', JSON.stringify(cart));}

function addToWish(name){
    if(!wishlist.includes(name)){wishlist.push(name);}
    localStorage.setItem('wishlist', JSON.stringify(wishlist));
    updateWish();
}
function updateWish(){localStorage.setItem('wishlist', JSON.stringify(wishlist));}

// Menu Dropdown
function toggleMenu(){document.getElementById('menuContent').classList.toggle('show');}
window.onclick = function(e){if(!e.target.matches('.menu-btn')){let menu=document.getElementById('menuContent'); if(menu.classList.contains('show')){menu.classList.remove('show');}}}

// Bottom Functions
function toggleCart(){alert('Cart clicked!')}
function toggleWishlist(){alert('Wishlist clicked!')}
function scrollToSearch(){document.getElementById('searchInput').scrollIntoView({behavior:'smooth'})}

// Search Filter
document.getElementById('searchInput').addEventListener('keyup',function(){
    let filter=this.value.toLowerCase();
    document.querySelectorAll('.card').forEach(card=>{
        let text=card.querySelector('h3').innerText.toLowerCase();
        card.style.display=text.includes(filter)?'':'none';
    });
});

// Random Ads Rotation
const ads = [
"🔥 20% OFF on Wireless Earbuds! 🔥",
"🎉 15% OFF on Smart LED Lamp! 🎉",
"💥 Buy 1 Get 1 Free on Bluetooth Speaker! 💥",
"✨ Flat 10% OFF on Mini Projector! ✨",
"🔥 Hot Sale: 25% OFF on Portable Power Bank! 🔥"
];
let adIndex=0;
setInterval(()=>{
    adIndex=(adIndex+1)%ads.length;
    document.getElementById('adsBarTop').innerText=ads[adIndex];
    document.getElementById('adsBarBottom').innerText=ads[adIndex];
},5000);

</script>
</body>
</html>
