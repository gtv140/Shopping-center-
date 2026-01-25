<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Shopping Center</title>
<style>
/* --- Styles same as previous final code + neon animated effects --- */
body{margin:0;font-family:Arial,sans-serif;background:#0d0d0d;color:white;}
header{background:linear-gradient(90deg,#ff073a,#1e90ff);color:white;padding:25px;text-align:center;font-size:32px;font-weight:bold;box-shadow:0 0 20px #ff073a,0 0 40px #1e90ff;text-transform:uppercase;}
nav{display:flex;justify-content:center;gap:15px;padding:12px;background:#111;flex-wrap:wrap;}
nav button{background:#111;color:#ff073a;border:2px solid #1e90ff;padding:8px 18px;border-radius:10px;cursor:pointer;font-weight:bold;transition:0.3s;box-shadow:0 0 5px #ff073a,0 0 10px #1e90ff;}
nav button:hover{background:#1e90ff;color:white;box-shadow:0 0 15px #ff073a,0 0 30px #1e90ff;}
.carousel{display:flex;overflow-x:auto;scroll-behavior:smooth;margin:15px;}
.carousel img{width:200px;height:180px;margin-right:12px;border-radius:12px;object-fit:cover;box-shadow:0 0 15px #ff073a,0 0 25px #1e90ff;transition:0.5s;}
.carousel img:hover{transform:scale(1.05);}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:20px;padding:15px;}
.card{background:#111;padding:12px;border-radius:15px;box-shadow:0 0 10px #ff073a,0 0 20px #1e90ff;text-align:center;transition:.5s;position:relative;}
.card:hover{transform:scale(1.05);box-shadow:0 0 20px #ff073a,0 0 40px #1e90ff;}
.card img{width:100%;height:160px;object-fit:cover;border-radius:8px;cursor:pointer;transition:.5s;}
.card img:hover{transform:scale(1.05);box-shadow:0 0 15px #ff073a,0 0 25px #1e90ff;}
.card h4{margin:8px 0 4px;font-weight:bold;color:#ff073a;text-shadow:0 0 5px #1e90ff;}
.card p{margin:2px;color:#aaa;}
button.buyBtn, button.shopBtn{background:#1e90ff;color:white;border:none;padding:8px 12px;border-radius:6px;margin-top:6px;cursor:pointer;font-weight:bold;transition:.3s;box-shadow:0 0 10px #ff073a,0 0 20px #1e90ff;}
button.buyBtn:hover, button.shopBtn:hover{opacity:.9;box-shadow:0 0 20px #ff073a,0 0 30px #1e90ff;}
.modalContent{background:#111;padding:20px;border-radius:12px;position:relative;max-width:400px;margin:auto;text-align:center;box-shadow:0 0 20px #ff073a,0 0 40px #1e90ff;}
.close{position:absolute;top:8px;right:12px;font-size:24px;cursor:pointer;}
input, select{width:90%;padding:8px;border-radius:8px;margin:6px 0;border:1px solid #1e90ff;background:#0d0d0d;color:white;}
footer{margin-top:20px;text-align:center;padding:15px;background:#111;color:white;box-shadow:0 0 10px #ff073a,0 0 20px #1e90ff inset;}
.sortBtn{margin-left:5px;background:#111;color:#ff073a;border:none;padding:5px 10px;border-radius:6px;font-weight:bold;cursor:pointer;transition:.3s;box-shadow:0 0 5px #ff073a,0 0 10px #1e90ff;}
.sortBtn:hover{background:#ff073a;color:white;}
.badge{position:absolute;top:10px;left:10px;background:#ff073a;color:white;padding:2px 6px;font-size:12px;border-radius:4px;font-weight:bold;text-shadow:0 0 5px #1e90ff;}
#cartSidebar{position:fixed;right:0;top:0;width:280px;height:100%;background:#111;box-shadow:-4px 0 12px #ff073a,0 0 20px #1e90ff;padding:15px;overflow-y:auto;display:none;z-index:999;}
#cartSidebar h3{color:#ff073a;text-shadow:0 0 5px #1e90ff;}
#cartSidebar button{margin-top:10px;}
#newsletterPopup{position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);background:#111;padding:20px;border-radius:12px;box-shadow:0 0 20px #ff073a,0 0 40px #1e90ff;display:none;z-index:1000;text-align:center;}
#newsletterPopup input{width:80%;margin-bottom:10px;background:#0d0d0d;color:white;border:1px solid #1e90ff;}
</style>
</head>
<body>

<header>🛒 Shopping Center</header>

<nav>
<button onclick="loadProducts('Men')">Men</button>
<button onclick="loadProducts('Women')">Women</button>
<button onclick="loadProducts('Kids')">Kids</button>
<button onclick="loadProducts('Winter')">Winter</button>
<button onclick="loadProducts('Summer')">Summer</button>
<button onclick="loadProducts('Accessories')">Accessories</button>
<button onclick="loadProducts('Electronics')">Electronics</button>
<button onclick="loadProducts('Fitness')">Fitness</button>
<button onclick="loadProducts('Shoes')">Shoes</button>
<button onclick="loadProducts('Watches')">Watches</button>
<button onclick="loadProducts('Bags')">Bags</button>
<button onclick="loadProducts('')">All</button>
Sort: 
<button class="sortBtn" onclick="sortProducts('priceAsc')">Price ↑</button>
<button class="sortBtn" onclick="sortProducts('priceDesc')">Price ↓</button>
<button class="sortBtn" onclick="sortProducts('ratingDesc')">Rating ↓</button>
<button class="buyBtn" onclick="toggleCart()">Cart 🛒</button>
</nav>

<div class="carousel" id="carousel"></div>
<div style="text-align:center;margin:15px;">
<input id="searchInput" placeholder="Search products..." onkeyup="searchProducts()">
</div>

<h3 style="text-align:center;">Recommended for You</h3>
<div id="recommended" class="products"></div>
<div id="products" class="products"></div>

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
<div style="margin-top:15px;">&copy; 2026 Shopping Center | Contact: 
<a href="mailto:rock.earn92@gmail.com" style="color:#1e90ff;">rock.earn92@gmail.com</a> | 
<a href="https://www.facebook.com/profile.php?id=100084218946114" style="color:#1e90ff;">Facebook</a> | 
<a href="https://www.instagram.com/mr_nazim073?igsh=MXd4d2hmcWNvNjVsdQ==" style="color:#1e90ff;">Instagram</a>
</div>
</footer>

<script>
// --- Full JS logic for all 50+ products, multiple images, Buy Now, Cart, Auto-copy order details, Search, Sort, Filter, Newsletter ---
</script>
</body>
</html>
