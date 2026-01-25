<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-app.js";
import { getFirestore, collection, getDocs, addDoc, doc } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-firestore.js";
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
async function loadProducts(filter=""){
  const box = document.getElementById("products");
  box.innerHTML = "";
  const snap = await getDocs(collection(db,"products"));
  snap.forEach(d=>{
    const p = d.data();
    if(filter && !p.name.toLowerCase().includes(filter.toLowerCase()) && !p.cat.toLowerCase().includes(filter.toLowerCase())) return;
    const card = document.createElement("div");
    card.className = "card";
    card.innerHTML = `
      <img src="${p.image}" onclick="preview('${p.name}','${p.price}','${p.image}')">
      <h4>${p.name}</h4>
      <p>Rs ${p.price}</p>
      <button onclick="buyNow('${p.name}',${p.price})">Buy Now</button>
      ${window.isAdmin ? `<button class="del" onclick="deleteProduct('${d.id}')">Delete</button>` : ``}
    `;
    box.appendChild(card);
  });
}

/* 🔥 PRODUCT PREVIEW */
window.preview=(n,p,img)=>{
  const m = document.getElementById("previewModal");
  m.style.display="flex";
  m.innerHTML=`<div class="modalContent">
    <span onclick="closePreview()" class="close">&times;</span>
    <img src="${img}">
    <h3>${n}</h3>
    <p>Rs ${p}</p>
    <button onclick="buyNow('${n}',${p})">Buy Now</button>
  </div>`;
};
window.closePreview=()=>document.getElementById("previewModal").style.display="none";

/* 🔥 BUY NOW FORM */
window.buyNow = (name,price)=>{
  const modal = document.getElementById("orderModal");
  modal.style.display="flex";
  modal.innerHTML=`<div class="modalContent">
    <span onclick="closeOrder()" class="close">&times;</span>
    <h3>Order: ${name}</h3>
    <p>Price: Rs ${price}</p>
    <input id="userName" placeholder="Your Name"><br>
    <input id="userLocation" placeholder="Location / Address"><br>
    <input id="userWhatsApp" placeholder="WhatsApp Number"><br>
    <input id="userContact" placeholder="Contact Number"><br>
    <input type="file" id="paymentProof"><br>
    <select id="paymentMethod">
      <option value="COD">Cash on Delivery</option>
      <option value="JazzCash">JazzCash (03705519562)</option>
      <option value="EasyPaisa">EasyPaisa (03379827882)</option>
    </select><br>
    <button onclick="submitOrder('${name}',${price})">Submit Order</button>
  </div>`;
};
window.closeOrder=()=>document.getElementById("orderModal").style.display="none";

/* 🔥 SUBMIT ORDER */
window.submitOrder = async (product,price)=>{
  const name=document.getElementById("userName").value;
  const loc=document.getElementById("userLocation").value;
  const whatsapp=document.getElementById("userWhatsApp").value;
  const contact=document.getElementById("userContact").value;
  const method=document.getElementById("paymentMethod").value;
  const proof=document.getElementById("paymentProof").files[0];

  if(!name||!loc||!whatsapp||!contact){alert("Fill all fields"); return;}

  let proofURL="";
  if(proof){ 
    const sRef=ref(storage,"proof/"+Date.now()+proof.name);
    await uploadBytes(sRef,proof);
    proofURL=await getDownloadURL(sRef);
  }

  await addDoc(collection(db,"orders"),{
    product,price,name,loc,whatsapp,contact,method,proof:proofURL,date:new Date().toISOString()
  });

  alert("Order submitted successfully!");
  closeOrder();
};

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
  loadProducts(document.getElementById("searchInput")?.value || "");
});

/* 🔥 ADD PRODUCT */
window.addProduct = async ()=>{
  const name = pName.value;
  const price = Number(pPrice.value);
  const cat = pCat.value;
  const file = pImage.files[0];
  if(!name || !price || !file){ alert("Fill all fields"); return; }

  const sRef = ref(storage,"products/"+Date.now()+file.name);
  await uploadBytes(sRef,file);
  const url = await getDownloadURL(sRef);

  await addDoc(collection(db,"products"),{name,price,cat,image:url});
  loadProducts(document.getElementById("searchInput")?.value || "");
};

/* 🔥 DELETE */
window.deleteProduct = async (id)=>{
  if(confirm("Delete product?")){
    await deleteDoc(doc(db,"products",id));
    loadProducts(document.getElementById("searchInput")?.value || "");
  }
};

/* 🔥 SEARCH */
window.searchProducts=()=>loadProducts(document.getElementById("searchInput").value);

window.onload=()=>{ loadProducts(); renderCart(); };
</script>

<style>
body{margin:0;font-family:Arial;background:#fff3e0}
header{background:#ff6f00;color:#fff;padding:18px;text-align:center;font-size:26px}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(170px,1fr));gap:15px;padding:15px}
.card{background:#fff;padding:10px;border-radius:10px;box-shadow:0 3px 8px #0003;text-align:center;transition:.3s}
.card:hover{transform:scale(1.05)}
.card img{width:100%;height:150px;object-fit:cover;border-radius:8px;cursor:pointer}
button{background:#ff6f00;color:#fff;border:none;padding:8px 12px;border-radius:6px;margin-top:5px;cursor:pointer}
.del{background:red}
#previewModal,#orderModal{display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:#0009;justify-content:center;align-items:center}
.modalContent{background:#fff;padding:20px;border-radius:10px;text-align:center;position:relative;max-width:300px;margin:auto}
.close{position:absolute;top:5px;right:10px;font-size:22px;cursor:pointer}
#adminBox,#adminPanel{display:none;margin-top:10px}
input, select{padding:5px;border-radius:6px;margin:5px 0;width:90%}
#searchInput{width:90%;padding:7px;margin:10px auto;display:block}
</style>
</head>

<body>
<header>🛒 Shopping Center</header>

<!-- SEARCH -->
<input id="searchInput" placeholder="Search products..." onkeyup="searchProducts()">

<!-- CATEGORY FILTER -->
<select id="pCat" onchange="searchProducts()">
  <option>All</option>
  <option>Men</option>
  <option>Women</option>
  <option>Accessories</option>
  <option>Electronics</option>
  <option>Fitness</option>
</select>

<!-- PRODUCTS GRID -->
<div class="products" id="products"></div>

<h3 style="padding-left:15px">🛍 Cart</h3>
<pre id="cart" style="padding-left:15px"></pre>
<button onclick="checkout()" style="margin-left:15px">Order via WhatsApp</button>

<!-- MODALS -->
<div id="previewModal"></div>
<div id="orderModal"></div>

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
<select id="pCat">
  <option>Men</option>
  <option>Women</option>
  <option>Accessories</option>
  <option>Electronics</option>
  <option>Fitness</option>
</select>
<input id="pImage" type="file"><br>
<button onclick="addProduct()">Add Product</button>
<button onclick="logoutAdmin()">Logout</button>
</div>
</footer>
</body>
</html>
