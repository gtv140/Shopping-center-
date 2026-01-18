<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial;background:#f4f4f4;color:#222}

/* HEADER */
header{background:#111;color:#fff;padding:15px;text-align:center}
header input{
  margin-top:10px;
  padding:8px;
  width:90%;
  max-width:400px;
  border-radius:5px;
  border:none;
}

/* CATEGORY ICONS */
.categories{
  display:flex;
  justify-content:center;
  flex-wrap:wrap;
  gap:10px;
  margin:12px 0;
}
.categories button{
  background:#eee;
  border:none;
  padding:10px;
  border-radius:50px;
  cursor:pointer;
  font-size:14px;
}

/* CART BUTTON */
#cartBtn{
  position:fixed;
  bottom:15px;
  right:15px;
  background:#000;
  color:#fff;
  padding:12px 16px;
  border-radius:50px;
  cursor:pointer;
  font-size:14px;
}

/* PRODUCTS */
.products{
  padding:20px;
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
  gap:16px;
}
.product{
  background:#fff;
  border-radius:10px;
  overflow:hidden;
  box-shadow:0 3px 10px rgba(0,0,0,.1);
  position:relative;
}
.product img{width:100%;height:180px;object-fit:cover}
.info{padding:10px}
.info h3{margin:0;font-size:15px}
.price{font-weight:bold;margin:5px 0}
.buttons a{
  display:block;
  text-align:center;
  margin-top:6px;
  padding:6px;
  border-radius:6px;
  color:#fff;
  text-decoration:none;
  font-size:13px;
}
.insta{background:#e1306c}
.fb{background:#1877f2}
.mail{background:#000}
.badge{
  position:absolute;
  top:10px;
  left:10px;
  background:#f00;
  color:#fff;
  padding:4px 6px;
  font-size:12px;
  border-radius:4px;
}

/* RECENT */
.recent{
  background:#fff;
  margin:20px;
  padding:15px;
  border-radius:10px;
}
.recent span{
  display:inline-block;
  background:#eee;
  padding:6px 10px;
  margin:4px;
  border-radius:20px;
  font-size:13px;
}

/* FOOTER */
footer{background:#111;color:#aaa;text-align:center;padding:12px;font-size:13px}
</style>
</head>

<body>

<header>
  <h1>Shopping Center</h1>
  <p>Simple • Premium • Smart Store</p>
  <input type="text" id="search" placeholder="Search products...">
</header>

<div class="categories">
<button onclick="filterCategory('All')">🏷️ All</button>
<button onclick="filterCategory('Electronics')">📱 Electronics</button>
<button onclick="filterCategory('Fashion')">👟 Fashion</button>
<button onclick="filterCategory('Audio')">🎧 Audio</button>
<button onclick="filterCategory('Accessories')">⌚ Accessories</button>
</div>

<section class="products" id="productList">

<!-- PRODUCTS START -->

<!-- Electronics -->
<div class="product" data-name="Smart Phone" data-category="Electronics">
<div class="badge">🔥 Trending</div>
<img src="https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?w=800">
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

<div class="product" data-name="Smart Watch" data-category="Accessories">
<div class="badge">💥 Sale</div>
<img src="https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=800">
<div class="info">
<h3>Smart Watch</h3>
<div class="price">PKR 13,999</div>
<div class="buttons">
<a class="insta" href="https://www.instagram.com/shoppingcenter664?igsh=MW0zZTZoOTB4aXc1Mg==" target="_blank">Instagram</a>
<a class="fb" href="https://www.facebook.com/profile.php?id=61581475052443" target="_blank">Facebook</a>
<a class="mail" href="mailto:rock.earn92@gmail.com">Gmail</a>
</div>
<button onclick="addToCart('Smart Watch')">Add to Cart</button>
</div>
</div>

<div class="product" data-name="Running Shoes" data-category="Fashion">
<div class="badge">⭐ Top Rated</div>
<img src="https://images.unsplash.com/photo-1542291026-7eec264c27ff?w=800">
<div class="info">
<h3>Running Shoes</h3>
<div class="price">PKR 9,999</div>
<div class="buttons">
<a class="insta" href="https://www.instagram.com/shoppingcenter664?igsh=MW0zZTZoOTB4aXc1Mg==" target="_blank">Instagram</a>
<a class="fb" href="https://www.facebook.com/profile.php?id=61581475052443" target="_blank">Facebook</a>
<a class="mail" href="mailto:rock.earn92@gmail.com">Gmail</a>
</div>
<button onclick="addToCart('Running Shoes')">Add to Cart</button>
</div>
</div>

<div class="product" data-name="Headphones" data-category="Audio">
<div class="badge">🔥 Trending</div>
<img src="https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=800">
<div class="info">
<h3>Headphones</h3>
<div class="price">PKR 7,499</div>
<div class="buttons">
<a class="insta" href="https://www.instagram.com/shoppingcenter664?igsh=MW0zZTZoOTB4aXc1Mg==" target="_blank">Instagram</a>
<a class="fb" href="https://www.facebook.com/profile.php?id=61581475052443" target="_blank">Facebook</a>
<a class="mail" href="mailto:rock.earn92@gmail.com">Gmail</a>
</div>
<button onclick="addToCart('Headphones')">Add to Cart</button>
</div>
</div>

<!-- Add 16+ more products in similar format -->

</section>

<div class="recent">
<strong>Recently Viewed:</strong><br>
<div id="recentItems"></div>
</div>

<footer>
© 2026 Shopping Center
</footer>

<div id="cartBtn">🛒 Cart</div>

<script>
// CART (localStorage)
let cart = JSON.parse(localStorage.getItem("cart")) || [];

function addToCart(name){
  cart.push(name);
  localStorage.setItem("cart",JSON.stringify(cart));
  alert(name+" added to cart");
  addRecent(name);
}

// SEARCH
document.getElementById("search").addEventListener("keyup",function(){
  let val=this.value.toLowerCase();
  document.querySelectorAll(".product").forEach(p=>{
    p.style.display=p.dataset.name.toLowerCase().includes(val)?"block":"none";
  });
});

// CATEGORY FILTER
function filterCategory(cat){
  document.querySelectorAll(".product").forEach(p=>{
    p.style.display=(cat=="All" || p.dataset.category==cat)?"block":"none";
  });
}

// RECENT VIEW
function addRecent(name){
  let recent=JSON.parse(localStorage.getItem("recent"))||[];
  if(!recent.includes(name)){
    recent.unshift(name);
    if(recent.length>5) recent.pop();
    localStorage.setItem("recent",JSON.stringify(recent));
  }
  showRecent();
}

function showRecent(){
  let recent=JSON.parse(localStorage.getItem("recent"))||[];
  document.getElementById("recentItems").innerHTML=
    recent.map(i=>`<span>${i}</span>`).join("");
}
showRecent();

// CART VIEW
document.getElementById("cartBtn").onclick=function(){
  alert("Cart Items:\n"+(cart.length?cart.join(", "):"Cart empty"));
};
</script>

</body>
</html>
