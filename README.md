<html>
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-app.js";
import { getFirestore, collection, getDocs, addDoc, deleteDoc, doc } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-firestore.js";
import { getAuth, signInWithEmailAndPassword, signOut, setPersistence, browserLocalPersistence, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-auth.js";

/* 🔥 Firebase config */
const firebaseConfig = {
  apiKey: "AIzaSyAL7_6DTdz14ySlLQ1jjuQC4WdO4mpRZKY",
  authDomain: "shopping-center-9.firebaseapp.com",
  projectId: "shopping-center-9",
  storageBucket: "shopping-center-9.appspot.com",
  messagingSenderId: "33427127023",
  appId: "1:33427127023:web:a478af6499f28f84d9391a"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
const auth = getAuth(app);
setPersistence(auth, browserLocalPersistence);

/* 🔥 CART localStorage FIX */
let cart = JSON.parse(localStorage.getItem("cart")) || [];

function saveCart(){
  localStorage.setItem("cart", JSON.stringify(cart));
}

/* 🔥 LOAD PRODUCTS */
async function loadProducts(){
  const box = document.getElementById("products");
  box.innerHTML = "";
  const snap = await getDocs(collection(db,"products"));
  snap.forEach(d=>{
    const p = d.data();
    box.innerHTML += `
      <div class="card">
        <img src="${p.image}">
        <h4>${p.name}</h4>
        <p>Rs ${p.price}</p>
        <button onclick="addToCart('${p.name}',${p.price})">Add to Cart</button>
      </div>`;
  });
}

/* 🔥 CART */
window.addToCart = (n,p)=>{
  cart.push({n,p});
  saveCart();
  renderCart();
};

function renderCart(){
  document.getElementById("cart").innerText =
    cart.map(i=>`${i.n} - Rs ${i.p}`).join("\n");
}
window.checkout = ()=>{
  if(!cart.length){alert("Cart empty");return;}
  let m = cart.map(i=>`${i.n} Rs ${i.p}`).join("%0A");
  window.open("https://wa.me/923000000000?text=Order%0A"+m);
};

/* 🔥 ADMIN LOGIN */
window.showAdmin=()=>document.getElementById("adminBox").style.display="block";
window.loginAdmin=()=>{
  signInWithEmailAndPassword(
    auth,
    adminEmail.value,
    adminPass.value
  );
};
window.logoutAdmin=()=>signOut(auth);

/* 🔥 ADMIN AUTH CHECK */
onAuthStateChanged(auth,u=>{
  document.getElementById("adminPanel").style.display = u?"block":"none";
});

/* 🔥 AUTO LOAD */
window.onload=()=>{
  loadProducts();
  renderCart();
};
</script>

<style>
body{margin:0;font-family:Arial;background:#fff3e0}
header{background:#ff6f00;color:#fff;padding:18px;text-align:center;font-size:26px}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:15px;padding:15px}
.card{background:#fff;padding:10px;border-radius:10px;box-shadow:0 3px 8px #0003;text-align:center}
.card img{width:100%;height:160px;object-fit:cover;border-radius:8px}
button{background:#ff6f00;color:#fff;border:none;padding:8px 14px;border-radius:6px}
footer{text-align:center;padding:15px;color:#555}
#adminBox{display:none}
pre{background:#fff;padding:10px;border-radius:8px}
</style>
</head>

<body>

<header>🛒 Shopping Center</header>

<div class="products" id="products">

<!-- 🔥 DEMO PRODUCTS (STATIC BACKUP) -->
<div class="card">
<img src="https://images.unsplash.com/photo-1523381210434-271e8be1f52b">
<h4>Men T‑Shirt</h4><p>Rs 1200</p>
<button onclick="addToCart('Men T‑Shirt',1200)">Add</button>
</div>

<div class="card">
<img src="https://images.unsplash.com/photo-1593032465171-8c9c3c57aab1">
<h4>Women Bag</h4><p>Rs 2500</p>
<button onclick="addToCart('Women Bag',2500)">Add</button>
</div>

<div class="card">
<img src="https://images.unsplash.com/photo-1585386959984-a4155228f7c1">
<h4>Headphones</h4><p>Rs 3500</p>
<button onclick="addToCart('Headphones',3500)">Add</button>
</div>

<div class="card">
<img src="https://images.unsplash.com/photo-1596461404969-9ae70f2830c1">
<h4>Sunglasses</h4><p>Rs 1800</p>
<button onclick="addToCart('Sunglasses',1800)">Add</button>
</div>

</div>

<h3 style="padding-left:15px">🛍 Your Cart</h3>
<pre id="cart"></pre>
<button onclick="checkout()">Order via WhatsApp</button>

<footer>
<button onclick="showAdmin()">Admin Login</button>

<div id="adminBox">
<input id="adminEmail" placeholder="Email"><br>
<input id="adminPass" type="password" placeholder="Password"><br>
<button onclick="loginAdmin()">Login</button>
</div>

<div id="adminPanel">
<p>✅ Admin Logged In</p>
<button onclick="logoutAdmin()">Logout</button>
</div>
</footer>

</body>
</html>
