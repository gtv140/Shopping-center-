<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center Ultimate 🛒</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<!-- Firebase SDKs -->
<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-app.js";
import { getFirestore, collection, getDocs, addDoc, deleteDoc, doc } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-firestore.js";
import { getStorage, ref, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-storage.js";
import { getAuth, signInWithEmailAndPassword, signOut, setPersistence, browserLocalPersistence, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-auth.js";

/* 🔥 Firebase Config */
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
const storage = getStorage(app);
const auth = getAuth(app);
setPersistence(auth, browserLocalPersistence);

/* 🔥 CART */
let cart = JSON.parse(localStorage.getItem("cart")) || [];
function saveCart(){ localStorage.setItem("cart", JSON.stringify(cart)); }

/* 🔥 LOAD PRODUCTS */
async function loadProducts(){
  const box = document.getElementById("products");
  box.innerHTML = "";
  const snap = await getDocs(collection(db,"products"));
  snap.forEach(d=>{
    const p = d.data();
    const card = document.createElement("div");
    card.className = "card";
    card.innerHTML = `
      <img src="${p.image}">
      <h4>${p.name}</h4>
      <p>Rs ${p.price}</p>
      <button onclick="addToCart('${p.name}',${p.price})">Add to Cart</button>
      ${document.getElementById("adminPanel")?.style.display=="block"?`<button style="background:red" onclick="deleteProduct('${d.id}')">Delete</button>`:""}
    `;
    box.appendChild(card);
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
  if(!cart.length){alert("Cart empty"); return;}
  let m = cart.map(i=>`${i.n} Rs ${i.p}`).join("%0A");
  window.open("https://wa.me/923000000000?text=Order%0A"+m);
};

/* 🔥 ADMIN LOGIN */
window.showAdminLogin=()=>document.getElementById("adminBox").style.display="block";
window.loginAdmin=()=>{
  signInWithEmailAndPassword(auth,document.getElementById("adminEmail").value,document.getElementById("adminPass").value);
};
window.logoutAdmin=()=>signOut(auth);

/* 🔥 ADMIN CHECK */
onAuthStateChanged(auth,u=>{
  document.getElementById("adminPanel").style.display = u?"block":"none";
  loadProducts();
});

/* 🔥 ADD PRODUCT */
window.addProduct=async ()=>{
  const name=document.getElementById("pName").value;
  const price=parseFloat(document.getElementById("pPrice").value);
  const cat=document.getElementById("pCat").value;
  const file=document.getElementById("pImage").files[0];
  if(!name||!price||!file){alert("Fill all fields"); return;}
  const storageRef=ref(storage,"products/"+Date.now()+"_"+file.name);
  await uploadBytes(storageRef,file);
  const url=await getDownloadURL(storageRef);
  await addDoc(collection(db,"products"),{name,price,cat,image:url});
  loadProducts();
};

/* 🔥 DELETE PRODUCT */
window.deleteProduct=async (id)=>{
  if(confirm("Delete this product?")){
    await deleteDoc(doc(db,"products",id));
    loadProducts();
  }
};

/* 🔥 INITIAL LOAD */
window.addEventListener("DOMContentLoaded",()=>{
  loadProducts();
  renderCart();
});
</script>

<script src="https://www.google.com/recaptcha/api.js" async defer></script>

<style>
body{margin:0;font-family:Arial;background:#fff3e0;}
header{background:#ff6f00;color:white;padding:20px;text-align:center;font-size:28px;font-weight:bold;}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:15px;padding:15px}
.card{background:white;padding:10px;border-radius:10px;box-shadow:0 3px 8px #0003;text-align:center;transition:0.3s}
.card:hover{transform:scale(1.05)}
.card img{width:100%;height:160px;object-fit:cover;border-radius:8px}
button{background:#ff6f00;color:white;border:none;padding:8px 12px;border-radius:6px;margin-top:5px;cursor:pointer}
button:hover{background:#e03e00}
footer{text-align:center;padding:15px;color:#555}
#adminBox{display:none;margin-top:10px}
#adminPanel{display:none;margin-top:10px;background:#fff3e0;padding:10px;border-radius:8px;box-shadow:0 3px 8px #0002;}
</style>
</head>

<body>
<header>🛒 Shopping Center Ultimate</header>

<!-- PRODUCTS GRID -->
<div class="products" id="products">
<!-- 50+ demo products will load from Firebase -->
</div>

<h3 style="padding-left:15px">🛍 Your Cart</h3>
<pre id="cart" style="padding-left:15px"></pre>
<select id="payment" style="margin-left:15px">
  <option>Cash on Delivery</option>
  <option>JazzCash</option>
  <option>EasyPaisa</option>
</select>
<button onclick="checkout()" style="margin-left:15px">Order via WhatsApp</button>

<!-- FOOTER -->
<footer>
<button onclick="showAdminLogin()">Admin Login</button>

<div id="adminBox">
<input type="email" id="adminEmail" placeholder="Email"><br>
<input type="password" id="adminPass" placeholder="Password"><br>
<div class="g-recaptcha" data-sitekey="6LfSlVUsAAAAAN0px_NgtAZlzzJLc_ew4B5speTy"></div>
<button onclick="loginAdmin()">Login</button>
</div>

<div id="adminPanel">
<h3>Admin Panel</h3>
<input type="text" id="pName" placeholder="Product Name">
<input type="number" id="pPrice" placeholder="Price">
<select id="pCat">
  <option>Men</option><option>Women</option><option>Accessories</option>
  <option>Electronics</option><option>Fitness</option>
</select>
<input type="file" id="pImage"><br>
<button onclick="addProduct()">Add Product</button>
<button onclick="logoutAdmin()">Logout</button>
</div>

</footer>
</body>
</html>
