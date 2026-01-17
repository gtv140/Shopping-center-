<SHOP>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>SHOPPING CENTER</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@500&display=swap" rel="stylesheet">
<style>
body{margin:0;font-family:'Orbitron',Arial,sans-serif;background:#0a0a0a;color:#fff}
header{background:#000;padding:20px;text-align:center;box-shadow:0 0 30px #0ff}
header h1{color:#0ff;text-shadow:0 0 10px #0ff,0 0 20px #0ff,0 0 30px #0ff;font-size:36px;letter-spacing:2px}
.search-bar{margin:10px auto;text-align:center}
.search-bar input{padding:12px;width:80%;border-radius:12px;border:none;outline:none;box-shadow:0 0 10px #0ff;background:#111;color:#fff}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:25px;padding:25px}
.card{background:#111;border-radius:15px;padding:15px;text-align:center;box-shadow:0 0 20px #0ff;transition:0.4s;position:relative;overflow:hidden}
.card:hover{transform:scale(1.05);box-shadow:0 0 50px #0ff}
.card img{width:100%;height:220px;object-fit:cover;border-radius:12px;transition:0.3s}
.card img:hover{transform:scale(1.05)}
.price{color:#0f0;font-weight:bold;font-size:18px;margin:10px 0}
.btns a, .btn-add, .btn-wish{display:block;margin:6px 0;padding:12px;border-radius:8px;text-decoration:none;color:#fff;font-weight:bold;transition:0.2s;text-align:center;cursor:pointer;box-shadow:0 0 8px #0ff}
.btn-add{background:#0ff;color:#000}
.btn-wish{background:#e1306c;color:#fff}
.btns a:hover, .btn-add:hover, .btn-wish:hover{opacity:0.85;transform:scale(1.05)}
.gmail{background:#d93025}
.insta{background:#e1306c}
.fb{background:#1877f2}
.wa{background:#25d366}
.qr{max-width:100px;margin:10px auto;border-radius:12px;display:block;box-shadow:0 0 10px #0ff}
.badge{position:absolute;top:10px;left:10px;background:#ff0;color:#000;padding:5px 10px;font-weight:bold;border-radius:6px;box-shadow:0 0 10px #ff0;font-size:12px;text-transform:uppercase}
.about{background:#111;margin:20px;padding:20px;border-radius:12px;box-shadow:0 0 20px #0ff;text-align:center}
.about h2{color:#0ff;margin-bottom:10px;text-shadow:0 0 5px #0ff}
.about p{color:#fff;font-size:16px}
.bottom-bar{position:fixed;bottom:0;left:0;width:100%;background:#111;display:flex;justify-content:space-around;align-items:center;padding:10px 0;box-shadow:0 -2px 20px #0ff;z-index:1000;border-top:2px solid #0ff}
.bottom-bar a{color:#fff;font-weight:bold;text-decoration:none;text-align:center;font-size:14px;padding:8px 10px;border-radius:10px;box-shadow:0 0 8px #0ff;transition:0.2s}
.bottom-bar a:hover{transform:scale(1.1);box-shadow:0 0 20px #0ff}
</style>
</head>
<body>

<header>
<h1>SHOPPING CENTER</h1>
<p style="color:#0ff;">Luxury Neon Premium Shop – Click & Order</p>
<div class="search-bar">
<input type="text" id="searchInput" placeholder="Search products...">
</div>
</header>

<section class="products" id="productContainer">

<!-- Men Product -->
<div class="card" data-category="Men">
<div class="badge">New</div>
<img src="https://i.ibb.co/3Y0F8xS/men-wallet.jpg" alt="Men Leather Wallet">
<h3>Men Leather Wallet</h3>
<p class="price">Rs 1,299</p>
<img class="qr" src="https://i.ibb.co/KxqG2gX/qr-men-wallet.png" alt="Instagram QR">
<div class="btns">
<button class="btn-add" onclick="addToCart('Men Leather Wallet',1299)">Add to Cart</button>
<button class="btn-wish" onclick="addToWish('Men Leather Wallet')">❤ Wishlist</button>
<a class="wa" href="https://wa.me/?text=Order%20Men%20Leather%20Wallet%20Rs%201,299" target="_blank">WhatsApp</a>
<a class="insta" href="https://ig.me/m/shoppingcenter664?text=Order%20Men%20Leather%20Wallet%20Rs%201,299" target="_blank">Instagram</a>
<a class="fb" href="https://m.me/61581475052443?text=Order%20Men%20Leather%20Wallet%20Rs%201,299" target="_blank">Facebook</a>
<a class="gmail" href="mailto:rock.earn92@gmail.com?subject=Order Men Leather Wallet&body=I want to order Men Leather Wallet Rs 1,299">Gmail</a>
</div>
</div>

<!-- Women Product -->
<div class="card" data-category="Women">
<div class="badge" style="background:#e1306c;color:#fff;">Hot</div>
<img src="https://i.ibb.co/bRgWkXY/women-handbag.jpg" alt="Elegant Women Handbag">
<h3>Elegant Women Handbag</h3>
<p class="price">Rs 2,499</p>
<img class="qr" src="https://i.ibb.co/yWQm6tk/qr-women-handbag.png" alt="Instagram QR">
<div class="btns">
<button class="btn-add" onclick="addToCart('Elegant Women Handbag',2499)">Add to Cart</button>
<button class="btn-wish" onclick="addToWish('Elegant Women Handbag')">❤ Wishlist</button>
<a class="wa" href="https://wa.me/?text=Order%20Elegant%20Women%20Handbag%20Rs%202,499" target="_blank">WhatsApp</a>
<a class="insta" href="https://ig.me/m/shoppingcenter664?text=Order%20Elegant%20Women%20Handbag%20Rs%202,499" target="_blank">Instagram</a>
<a class="fb" href="https://m.me/61581475052443?text=Order%20Elegant%20Women%20Handbag%20Rs%202,499" target="_blank">Facebook</a>
<a class="gmail" href="mailto:rock.earn92@gmail.com?subject=Order Women Handbag&body=I want to order Elegant Women Handbag Rs 2,499">Gmail</a>
</div>
</div>

</section>

<!-- About Section -->
<div class="about">
<h2>About SHOPPING CENTER</h2>
<p>Welcome to SHOPPING CENTER – your ultimate destination for luxury and premium products. Experience our neon-themed exclusive collection of Men, Women, Accessories, and Gadgets with a Shopify-style shopping feel. Click, order, and enjoy our fully interactive cart, wishlist, and instant messaging options. Shop smart, shop luxury!</p>
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
<p>© 2026 SHOPPING CENTER</p>
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
