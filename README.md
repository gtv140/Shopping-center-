<SHOPPING CENTER>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>SHOPPING CENTER</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body{margin:0;font-family:Arial;background:#111;color:#fff}
header{background:#000;padding:20px;text-align:center;box-shadow:0 0 20px #0ff}
header h1{color:#0ff;text-shadow:0 0 10px #0ff,0 0 20px #0ff,0 0 30px #0ff}
.search-bar{margin:10px auto;text-align:center}
.search-bar input{padding:10px;width:80%;border-radius:8px;border:none;outline:none}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(230px,1fr));gap:20px;padding:20px}
.card{background:#1c1c1c;border-radius:12px;padding:15px;text-align:center;box-shadow:0 0 20px #0ff;transition:0.3s}
.card:hover{transform:scale(1.05);box-shadow:0 0 40px #0ff}
.card img{width:100%;height:200px;object-fit:cover;border-radius:10px}
.price{color:#0f0;font-weight:bold;font-size:18px;margin:5px 0}
.btns a{display:block;margin:6px 0;padding:10px;border-radius:6px;text-decoration:none;color:#fff;font-weight:bold;transition:0.2s}
.btns a:hover{opacity:0.8;transform:scale(1.05)}
.gmail{background:#d93025}
.insta{background:#e1306c}
.fb{background:#1877f2}
.wa{background:#25d366}
.qr{max-width:120px;margin:10px auto;border-radius:10px;display:block}
footer{text-align:center;padding:15px;background:#000;box-shadow:0 -2px 20px #0ff}
.login-form, .signup-form{background:#1c1c1c;padding:20px;margin:20px auto;border-radius:12px;width:90%;max-width:400px;text-align:center;box-shadow:0 0 20px #0ff}
.login-form input, .signup-form input{padding:10px;margin:8px 0;width:90%;border:none;border-radius:6px;outline:none}
.login-form button, .signup-form button{padding:10px 15px;margin-top:10px;background:#0ff;border:none;color:#000;font-weight:bold;border-radius:6px;cursor:pointer;transition:0.2s}
.login-form button:hover, .signup-form button:hover{opacity:0.8;transform:scale(1.05)}
.cart-container{position:fixed;top:20px;right:20px;background:#1c1c1c;padding:15px;border-radius:12px;box-shadow:0 0 20px #0ff;max-width:300px;display:none}
.cart-container h3{text-align:center;color:#0ff;margin-bottom:10px}
.cart-item{display:flex;justify-content:space-between;margin:5px 0}
.cart-item span{color:#0f0}
</style>
</head>
<body>

<header>
<h1>SHOPPING CENTER</h1>
<p>Click & Order – Neon Premium Shop</p>
<div class="search-bar">
<input type="text" id="searchInput" placeholder="Search products...">
</div>
</header>

<!-- LOGIN / SIGNUP -->
<div class="login-form" id="loginForm">
<h2>Login</h2>
<input type="text" id="loginUser" placeholder="Username">
<input type="password" id="loginPass" placeholder="Password">
<button onclick="login()">Login</button>
<p>New user? <a href="#" onclick="showSignup()">Signup</a></p>
</div>

<div class="signup-form" id="signupForm" style="display:none;">
<h2>Signup</h2>
<input type="text" id="signupUser" placeholder="Username">
<input type="password" id="signupPass" placeholder="Password">
<button onclick="signup()">Signup</button>
<p>Already have account? <a href="#" onclick="showLogin()">Login</a></p>
</div>

<!-- Products Section -->
<section class="products" id="productContainer" style="display:none;">

<!-- Sample Men Product -->
<div class="card" data-category="Men">
<img src="https://cdn.pixabay.com/photo/2016/11/19/14/00/wallet-1838071_640.jpg" alt="Men Leather Wallet">
<h3>Men Leather Wallet</h3>
<p class="price">Rs 1,299</p>
<img class="qr" src="https://chart.googleapis.com/chart?chs=150x150&cht=qr&chl=https://instagram.com/shoppingcenter664&choe=UTF-8" alt="Instagram QR">
<div class="btns">
<a class="wa" href="https://wa.me/?text=Order%20Men%20Leather%20Wallet%20Rs%201,299" target="_blank">WhatsApp</a>
<a class="insta" href="https://ig.me/m/shoppingcenter664?text=Order%20Men%20Leather%20Wallet%20Rs%201,299" target="_blank">Instagram</a>
<a class="fb" href="https://m.me/61581475052443?text=Order%20Men%20Leather%20Wallet%20Rs%201,299" target="_blank">Facebook</a>
<a class="gmail" href="mailto:rock.earn92@gmail.com?subject=Order Men Leather Wallet&body=I want to order Men Leather Wallet Rs 1,299">Gmail</a>
</div>
</div>

<!-- Sample Women Product -->
<div class="card" data-category="Women">
<img src="https://cdn.pixabay.com/photo/2016/11/21/15/49/handbag-1845582_640.jpg" alt="Women Handbag">
<h3>Elegant Women Handbag</h3>
<p class="price">Rs 2,499</p>
<img class="qr" src="https://chart.googleapis.com/chart?chs=150x150&cht=qr&chl=https://instagram.com/shoppingcenter664&choe=UTF-8" alt="Instagram QR">
<div class="btns">
<a class="wa" href="https://wa.me/?text=Order%20Elegant%20Women%20Handbag%20Rs%202,499" target="_blank">WhatsApp</a>
<a class="insta" href="https://ig.me/m/shoppingcenter664?text=Order%20Elegant%20Women%20Handbag%20Rs%202,499" target="_blank">Instagram</a>
<a class="fb" href="https://m.me/61581475052443?text=Order%20Elegant%20Women%20Handbag%20Rs%202,499" target="_blank">Facebook</a>
<a class="gmail" href="mailto:rock.earn92@gmail.com?subject=Order Women Handbag&body=I want to order Elegant Women Handbag Rs 2,499">Gmail</a>
</div>
</div>

</section>

<!-- Cart -->
<div class="cart-container" id="cartContainer">
<h3>My Cart</h3>
<div id="cartItems"></div>
<p>Total: Rs <span id="cartTotal">0</span></p>
<button onclick="clearCart()">Clear Cart</button>
</div>

<footer>
<p>© 2026 SHOPPING CENTER</p>
</footer>

<script>
// Local Storage Login/Signup
function showSignup(){document.getElementById('loginForm').style.display='none';document.getElementById('signupForm').style.display='block';}
function showLogin(){document.getElementById('signupForm').style.display='none';document.getElementById('loginForm').style.display='block';}

function signup(){
let u=document.getElementById('signupUser').value;
let p=document.getElementById('signupPass').value;
if(u && p){localStorage.setItem('user_'+u,p);alert('Signup successful');showLogin();}else{alert('Enter username & password');}
}

function login(){
let u=document.getElementById('loginUser').value;
let p=document.getElementById('loginPass').value;
if(localStorage.getItem('user_'+u)===p){
alert('Login successful');document.getElementById('loginForm').style.display='none';document.getElementById('productContainer').style.display='grid';
loadCart();
}else{alert('Invalid credentials');}
}

// Cart System
let cart=[];
function loadCart(){
let c=JSON.parse(localStorage.getItem('cart'))||[];
cart=c;updateCartDisplay();
document.getElementById('cartContainer').style.display='block';
}
function updateCartDisplay(){
let container=document.getElementById('cartItems');
container.innerHTML='';
let total=0;
cart.forEach(item=>{
container.innerHTML+='<div class="cart-item">'+item.name+' x'+item.qty+' <span>Rs '+item.price*item.qty+'</span></div>';
total+=item.price*item.qty;
});
document.getElementById('cartTotal').innerText=total;
localStorage.setItem('cart',JSON.stringify(cart));
}
function clearCart(){cart=[];updateCartDisplay();alert('Cart cleared');}

// Search Filter
const searchInput=document.getElementById('searchInput');
searchInput.addEventListener('keyup',function(){
let filter=searchInput.value.toLowerCase();
let products=document.querySelectorAll('.card');
products.forEach(card=>{
let text=card.querySelector('h3').innerText.toLowerCase();
card.style.display=text.includes(filter)?'':'none';
});
});
</script>

</body>
</html>
