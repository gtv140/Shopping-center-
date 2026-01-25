<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

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
      ${window.isAdmin ? `<button class="del" onclick="deleteProduct('${d.id}')">Delete</button>` : ``}
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
  if(!cart.length){ alert("Cart empty"); return; }
  let msg = cart.map(i=>`${i.n} Rs ${i.p}`).join("%0A");
  window.open("https://wa.me/923000000000?text=Order%0A"+msg);
};

/* 🔥 ADMIN LOGIN */
window.showAdminLogin=()=>document.getElementById("adminBox").style.display="block";
window.loginAdmin=()=>{
  signInWithEmailAndPassword(
    auth,
    document.getElementById("adminEmail").value,
    document.getElementById("adminPass").value
  ).catch(e=>alert(e.message));
};
window.logoutAdmin=()=>signOut(auth);

/* 🔥 ADMIN STATE */
window.isAdmin = false;
onAuthStateChanged(auth,u=>{
  window.isAdmin = !!u;
  document.getElementById("adminPanel").style.display = u ? "block":"none";
  loadProducts();
});

/* 🔥 ADD PRODUCT */
window.addProduct = async ()=>{
  const name = pName.value;
  const price = Number(pPrice.value);
  const file = pImage.files[0];
  if(!name || !price || !file){ alert("Fill all fields"); return; }

  const sRef = ref(storage,"products/"+Date.now()+file.name);
  await uploadBytes(sRef,file);
  const url = await getDownloadURL(sRef);

  await addDoc(collection(db,"products"),{name,price,image:url});
  loadProducts();
};

/* 🔥 DELETE */
window.deleteProduct = async (id)=>{
  if(confirm("Delete product?")){
    await deleteDoc(doc(db,"products",id));
    loadProducts();
  }
};

window.onload=()=>{ loadProducts(); renderCart(); };
</script>

<style>
body{margin:0;font-family:Arial;background:#fff3e0}
header{background:#ff6f00;color:#fff;padding:18px;text-align:center;font-size:26px}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(170px,1fr));gap:15px;padding:15px}
.card{background:#fff;padding:10px;border-radius:10px;box-shadow:0 3px 8px #0003;text-align:center}
.card img{width:100%;height:150px;object-fit:cover;border-radius:8px}
button{background:#ff6f00;color:#fff;border:none;padding:8px 12px;border-radius:6px;margin-top:5px}
.del{background:red}
footer{text-align:center;padding:15px}
#adminBox,#adminPanel{display:none;margin-top:10px}
</style>
</head>

<body>
<header>🛒 Shopping Center</header>

<div class="products" id="products"></div>

<h3 style="padding-left:15px">🛍 Cart</h3>
<pre id="cart" style="padding-left:15px"></pre>
<button onclick="checkout()" style="margin-left:15px">Order via WhatsApp</button>

<footer>
<button onclick="showAdminLogin()">Admin Login</button>

<div id="adminBox">
<input id="adminEmail" placeholder="Email"><br>
<input id="adminPass" type="password" placeholder="Password"><br>
<button onclick="loginAdmin()">Login</button>
</div>

<div id="adminPanel">
<h3>Admin Panel</h3>
<input id="pName" placeholder="Product name">
<input id="pPrice" type="number" placeholder="Price">
<input id="pImage" type="file"><br>
<button onclick="addProduct()">Add Product</button>
<button onclick="logoutAdmin()">Logout</button>
</div>
</footer>
</body>
</html>
