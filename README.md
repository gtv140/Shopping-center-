<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>

<style>
*{box-sizing:border-box}
body{
  margin:0;
  font-family:system-ui,Arial;
  background:#f2f2f2;
  color:#222;
}

/* HEADER */
header{
  background:#111;
  color:#fff;
  padding:18px;
  text-align:center;
}
header h1{margin:0;font-size:26px}
header p{margin:4px 0 0;color:#bbb;font-size:14px}

/* CATEGORIES */
.categories{
  display:flex;
  gap:10px;
  padding:12px;
  overflow-x:auto;
  background:#fff;
}
.categories div{
  background:#000;
  color:#fff;
  padding:8px 14px;
  border-radius:20px;
  font-size:13px;
  white-space:nowrap;
}

/* BANNER */
.banner{
  background:linear-gradient(90deg,#000,#333);
  color:#fff;
  text-align:center;
  padding:15px;
  font-weight:bold;
}

/* PRODUCTS */
.products{
  padding:20px;
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
  gap:18px;
}
.product{
  background:#fff;
  border-radius:10px;
  overflow:hidden;
  box-shadow:0 4px 12px rgba(0,0,0,.08);
}
.product img{
  width:100%;
  height:180px;
  object-fit:cover;
}
.info{padding:12px}
.info h3{margin:0;font-size:16px}
.info p{margin:6px 0;font-weight:bold}

/* BUTTONS */
.buttons button{
  width:100%;
  margin-top:6px;
  padding:8px;
  border:none;
  border-radius:6px;
  cursor:pointer;
}
.insta{background:#e1306c;color:#fff}
.fb{background:#1877f2;color:#fff}
.mail{background:#000;color:#fff}

/* ABOUT */
.about{
  background:#fff;
  padding:20px;
  margin:20px;
  border-radius:10px;
  box-shadow:0 4px 10px rgba(0,0,0,.08);
}

/* FOOTER */
footer{
  background:#111;
  color:#aaa;
  text-align:center;
  padding:15px;
  font-size:13px;
}
</style>
</head>

<body>

<header>
  <h1>Shopping Center</h1>
  <p>Simple • Trusted • Premium Online Store</p>
</header>

<div class="categories">
  <div>Trending</div>
  <div>Electronics</div>
  <div>Fashion</div>
  <div>Beauty</div>
  <div>Accessories</div>
  <div>Gadgets</div>
</div>

<div class="banner">
🔥 Mega Sale – Flat Discounts on Trending Products 🔥
</div>

<section class="products">

<div class="product">
<img src="https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=800">
<div class="info">
<h3>Smart Watch</h3>
<p>$49</p>
<div class="buttons">
<button class="insta">Order on Instagram</button>
<button class="fb">Order on Facebook</button>
<button class="mail">Order on Gmail</button>
</div>
</div>
</div>

<div class="product">
<img src="https://images.unsplash.com/photo-1542291026-7eec264c27ff?w=800">
<div class="info">
<h3>Running Shoes</h3>
<p>$59</p>
<div class="buttons">
<button class="insta">Order on Instagram</button>
<button class="fb">Order on Facebook</button>
</div>
</div>
</div>

<div class="product">
<img src="https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=800">
<div class="info">
<h3>Headphones</h3>
<p>$39</p>
<div class="buttons">
<button class="insta">Order Now</button>
</div>
</div>
</div>

<div class="product">
<img src="https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?w=800">
<div class="info">
<h3>Smart Phone</h3>
<p>$199</p>
<div class="buttons">
<button class="fb">Buy Now</button>
</div>
</div>
</div>

<div class="product">
<img src="https://images.unsplash.com/photo-1585386959984-a4155224a1c1?w=800">
<div class="info">
<h3>Perfume</h3>
<p>$29</p>
<div class="buttons">
<button class="insta">Order</button>
</div>
</div>
</div>

<div class="product">
<img src="https://images.unsplash.com/photo-1593032465171-bb5a2c1f6d7c?w=800">
<div class="info">
<h3>Wireless Earbuds</h3>
<p>$45</p>
<div class="buttons">
<button class="fb">Order</button>
</div>
</div>
</div>

</section>

<div class="about">
<h3>About Shopping Center</h3>
<p>
Shopping Center ek simple aur trusted online store hai jahan
trending aur quality products best prices par milte hain.
Direct Instagram, Facebook aur Gmail ke zariye order karein.
</p>
</div>

<footer>
© 2026 Shopping Center — All Rights Reserved
</footer>

</body>
</html>
