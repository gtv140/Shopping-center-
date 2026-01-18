<SHOP>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>

<style>
*{box-sizing:border-box}
body{
  margin:0;
  font-family:system-ui,Arial;
  background:#f3f3f3;
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
.categories span{
  background:#000;
  color:#fff;
  padding:8px 14px;
  border-radius:20px;
  font-size:13px;
  white-space:nowrap;
}

/* SLIDER ADS */
.slider{
  background:#000;
  color:#fff;
  text-align:center;
  padding:12px;
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
.price{margin:6px 0;font-weight:bold}

/* BUTTONS */
.buttons a{
  display:block;
  text-align:center;
  margin-top:6px;
  padding:8px;
  border-radius:6px;
  color:#fff;
  text-decoration:none;
  font-size:14px;
}
.insta{background:#e1306c}
.fb{background:#1877f2}
.mail{background:#000}

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
  <p>Trusted • Simple • Online Store</p>
</header>

<div class="categories">
  <span>Trending</span>
  <span>Electronics</span>
  <span>Fashion</span>
  <span>Beauty</span>
  <span>Accessories</span>
  <span>Gadgets</span>
</div>

<div class="slider" id="slider">🔥 Flat 20% OFF on Trending Products 🔥</div>

<section class="products">

<div class="product">
<img src="https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=800">
<div class="info">
<h3>Smart Watch</h3>
<div class="price">PKR 13,999</div>
<div class="buttons">
<a class="insta" href="https://instagram.com/shoppingcenter664" target="_blank">Order on Instagram</a>
<a class="fb" href="https://facebook.com" target="_blank">Order on Facebook</a>
<a class="mail" href="mailto:rock.earn92@gmail.com">Order via Gmail</a>
</div>
</div>
</div>

<div class="product">
<img src="https://images.unsplash.com/photo-1542291026-7eec264c27ff?w=800">
<div class="info">
<h3>Running Shoes</h3>
<div class="price">PKR 9,999</div>
<div class="buttons">
<a class="insta" href="#">Order Now</a>
</div>
</div>
</div>

<div class="product">
<img src="https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=800">
<div class="info">
<h3>Headphones</h3>
<div class="price">PKR 7,499</div>
<div class="buttons">
<a class="fb" href="#">Buy Now</a>
</div>
</div>
</div>

<div class="product">
<img src="https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?w=800">
<div class="info">
<h3>Smart Phone</h3>
<div class="price">PKR 54,999</div>
<div class="buttons">
<a class="mail" href="mailto:rock.earn92@gmail.com">Order</a>
</div>
</div>
</div>

<div class="product">
<img src="https://images.unsplash.com/photo-1585386959984-a4155224a1c1?w=800">
<div class="info">
<h3>Perfume</h3>
<div class="price">PKR 4,499</div>
<div class="buttons">
<a class="insta" href="#">Order</a>
</div>
</div>
</div>

<div class="product">
<img src="https://images.unsplash.com/photo-1593032465171-bb5a2c1f6d7c?w=800">
<div class="info">
<h3>Wireless Earbuds</h3>
<div class="price">PKR 6,999</div>
<div class="buttons">
<a class="fb" href="#">Buy</a>
</div>
</div>
</div>

</section>

<div class="about">
<h3>About Shopping Center</h3>
<p>
Shopping Center ek trusted online store hai jahan aapko
trending aur quality products best prices par milte hain.
Direct Instagram, Facebook ya Gmail ke zariye order karein.
</p>
</div>

<footer>
© 2026 Shopping Center — All Rights Reserved
</footer>

<script>
const ads=[
"🔥 Flat 20% OFF on Trending Products 🔥",
"🚚 Free Delivery on Selected Items 🚚",
"💥 Limited Time Mega Sale 💥",
"⭐ Best Quality – Best Price ⭐"
];
let i=0;
setInterval(()=>{
  document.getElementById("slider").innerText=ads[i++%ads.length];
},2500);
</script>

</body>
</html>
