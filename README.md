<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>SHOPPING CENTER</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body{margin:0;font-family:Arial,sans-serif;background:#f8f8f8;color:#111}
header{background:#fff;padding:20px;text-align:center;box-shadow:0 2px 10px rgba(0,0,0,0.1)}
header h1{color:#333;font-size:32px;margin:0}
.search-bar{margin:15px auto;text-align:center}
.search-bar input{padding:10px;width:80%;border-radius:8px;border:1px solid #ccc;outline:none}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:20px;padding:20px}
.card{background:#fff;border-radius:10px;padding:15px;text-align:center;box-shadow:0 2px 10px rgba(0,0,0,0.1);transition:0.3s;position:relative}
.card:hover{transform:scale(1.03)}
.card img{width:100%;height:220px;object-fit:cover;border-radius:8px}
.price{color:#2a9d8f;font-weight:bold;font-size:18px;margin:10px 0}
.btns button, .btns a{display:block;margin:5px 0;padding:10px;border-radius:6px;text-decoration:none;color:#fff;font-weight:bold;cursor:pointer;border:none}
.btn-add{background:#2a9d8f}
.btn-wish{background:#e76f51}
.btns a{background:#264653;text-align:center}
.about{background:#fff;margin:20px;padding:20px;border-radius:10px;box-shadow:0 2px 10px rgba(0,0,0,0.1)}
.bottom-bar{position:fixed;bottom:0;left:0;width:100%;background:#fff;display:flex;justify-content:space-around;align-items:center;padding:10px 0;box-shadow:0 -2px 10px rgba(0,0,0,0.1);z-index:1000}
.bottom-bar a{color:#333;text-decoration:none;font-size:14px;text-align:center}
.bottom-bar a:hover{opacity:0.7}
</style>
</head>
<body>

<header>
<h1>SHOPPING CENTER</h1>
<p style="color:#555;">Premium Online Shop – Click & Order</p>
<div class="search-bar">
<input type="text" id="searchInput" placeholder="Search products...">
</div>
</header>

<section class="products" id="productContainer">

<!-- Men Product -->
<div class="card" data-category="Men">
<img src="https://i.ibb.co/3Y0F8xS/men-wallet.jpg" alt="Men Leather Wallet">
<h3>Men Leather Wallet</h3>
<p class="price">Rs 1,299</p>
<div class="btns">
<button class="btn-add" onclick="addToCart('Men Leather Wallet',1299)">Add to Cart</button>
<button class="btn-wish" onclick="addToWish('Men Leather Wallet')">❤ Wishlist</button>
<a href="https://wa.me/?text=Order%20Men%20Leather%20Wallet%20Rs%201,299" target="_blank">WhatsApp</a>
<a href="https://ig.me/m/shoppingcenter664?text=Order%20Men%20Leather%20Wallet%20Rs%201,299" target="_blank">Instagram</a>
<a href="https://m.me/61581475052443?text=Order%20Men%20Leather%20Wallet%20Rs%201,299" target="_blank">Facebook</a>
<a href="mailto:rock.earn92@gmail.com?subject=Order Men Leather Wallet&body=I want to order Men Leather Wallet Rs 1,299">Gmail</a>
</div>
</div>

<!-- Women Product -->
<div class="card" data-category="Women">
<img src="https://i.ibb.co/bRgWkXY/women-handbag.jpg" alt="Elegant Women Handbag">
<h3>Elegant Women Handbag</h3>
<p class="price">Rs 2,499</p>
<div class="btns">
<button class="btn-add" onclick="addToCart('Elegant Women Handbag',2499)">Add to Cart</button>
<button class="btn-wish" onclick="addToWish('Elegant Women Handbag')">❤ Wishlist</button>
<a href="https://wa.me/?text=Order%20Elegant%20Women%20Handbag%20Rs%202,499" target="_blank">WhatsApp</a>
<a href="https://ig.me/m/shoppingcenter664?text=Order%20Elegant%20Women%20Handbag%20Rs%202,499" target="_blank">Instagram</a>
<a href="https://m.me/61581475052443?text=Order%20Elegant%20Women%20Handbag%20Rs%202,499" target="_blank">Facebook</a>
<a href="mailto:rock.earn92@gmail.com?subject=Order Women Handbag&body=I want to order Elegant Women Handbag Rs 2,499">Gmail</a>
</div>
</div>

</section>

<!-- About Section -->
<div class="about">
<h2>About SHOPPING CENTER</h2>
<p>Welcome to SHOPPING CENTER – your premium destination for quality products. Browse, order, and enjoy our simple, elegant online shopping experience. Cart and wishlist fully functional. Shop smart, shop premium!</p>
</div>

<!-- Bottom Icons Bar -->
<div class="bottom-bar">
<a href="#" onclick="scrollToSearch()">🔍 Search</a>
<a href="#" onclick="toggleWishlist()">❤ Wishlist</a>
<a href="#" onclick="toggleCart()">🛒 Cart</a>
<a href="https://wa.me/?text=Hello%20SHOPPING%20CENTER" target="_blank">💬 WhatsApp</a>
<a href="https://ig.me/m/shoppingcenter664" target="_blank">📸 Instagram</a>
<a href="https://m.me/61581475052443" target="_blank">📘 Facebook</a>
<a href="mailto:rock.earn92@gmail.com">✉️ Gmail</a>
</div>

<footer>
<p style="text-align:center;padding:10px;color:#555;">© 2026 SHOPPING CENTER</p>
</footer>

<script>
// Cart & Wishlist System
let cart = JSON.parse(localStorage.getItem('cart')) || [];
let wishlist = JSON.parse(localStorage.getItem('wishlist')) || [];

function addToCart(name, price){
    let item = cart.find(i=>i.name===name);
    if(item){item.qty += 1;} else {cart.push({name:name, price:price, qty:1});}
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

// Bottom Icon Functions
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
</script>

</body>
</html>
