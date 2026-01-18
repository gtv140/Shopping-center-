<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ShopCenter - Online Store</title>

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:Arial,sans-serif}
body{background:#f4f4f4}

header{
display:flex;justify-content:space-between;align-items:center;
padding:20px;background:#111;color:#fff
}
header .logo{font-size:22px;font-weight:bold}
header nav a{color:#fff;margin-left:15px;text-decoration:none}
header nav a:hover{color:#f39c12}

.hero{
text-align:center;padding:90px 20px;
background:url('https://source.unsplash.com/1600x600/?shopping,mall') center/cover no-repeat;
color:white
}
.hero h1{font-size:42px}
.hero button{
margin-top:20px;padding:12px 30px;
background:#f39c12;border:none;color:#fff;font-size:16px;cursor:pointer
}

.products{padding:60px 20px;text-align:center}
.products h2{margin-bottom:30px;font-size:30px}

.product-grid{
display:flex;gap:30px;justify-content:center;flex-wrap:wrap
}
.product{
background:#fff;width:260px;padding:20px;border-radius:12px;
box-shadow:0 6px 15px rgba(0,0,0,.1);transition:.3s
}
.product:hover{transform:translateY(-6px)}
.product img{
width:100%;height:180px;object-fit:cover;border-radius:10px
}
.product h3{margin:12px 0;font-size:18px}
.product p{font-weight:bold;color:#27ae60}
.product button{
margin-top:10px;padding:10px;width:100%;
background:#111;color:#fff;border:none;cursor:pointer;border-radius:6px
}
.product button:hover{background:#f39c12}

footer{
margin-top:50px;background:#111;color:#fff;
text-align:center;padding:20px
}
</style>
</head>

<body>

<header>
<div class="logo">ShopCenter</div>
<nav>
<a href="#">Home</a>
<a href="#">Products</a>
<a href="#">Contact</a>
</nav>
</header>

<section class="hero">
<h1>ShopCenter Online Mall</h1>
<p>Shop Like Shopify ✨</p>
<button>Start Shopping</button>
</section>

<section class="products">
<h2>Featured Products</h2>

<div class="product-grid">

<div class="product">
<img src="https://source.unsplash.com/400x300/?wireless,headphones" alt="Headphones">
<h3>Wireless Headphones</h3>
<p>$29.99</p>
<button>Add to Cart</button>
</div>

<div class="product">
<img src="https://source.unsplash.com/400x300/?smartwatch" alt="Smart Watch">
<h3>Smart Watch</h3>
<p>$39.99</p>
<button>Add to Cart</button>
</div>

<div class="product">
<img src="https://source.unsplash.com/400x300/?gaming,mouse" alt="Mouse">
<h3>Gaming Mouse</h3>
<p>$24.99</p>
<button>Add to Cart</button>
</div>

<div class="product">
<img src="https://source.unsplash.com/400x300/?shoes,sneakers" alt="Shoes">
<h3>Sport Sneakers</h3>
<p>$59.99</p>
<button>Add to Cart</button>
</div>

<div class="product">
<img src="https://source.unsplash.com/400x300/?backpack,bag" alt="Bag">
<h3>Stylish Backpack</h3>
<p>$34.99</p>
<button>Add to Cart</button>
</div>

<div class="product">
<img src="https://source.unsplash.com/400x300/?perfume,beauty" alt="Perfume">
<h3>Luxury Perfume</h3>
<p>$44.99</p>
<button>Add to Cart</button>
</div>

</div>
</section>

<footer>
<p>© 2026 ShopCenter — Shopify Style Store</p>
</footer>

<script>
document.querySelectorAll("button").forEach(btn=>{
btn.onclick=()=>alert("Product added to cart 🛒");
});
</script>

</body>
</html>
