<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center 🛒</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<!-- Firebase SDKs -->
<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-app.js";
import { getFirestore, collection, getDocs, addDoc, deleteDoc, doc } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-firestore.js";
import { getStorage, ref, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-storage.js";
import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-auth.js";

// Firebase config
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

// Cart
let cart = [];

// =================== Admin Login ===================
window.loginAdmin = function(){
  const email = document.getElementById("adminEmail").value;
  const pass = document.getElementById("adminPassword").value;
  signInWithEmailAndPassword(auth, email, pass)
    .then(() => {
      document.getElementById("adminPanel").style.display="block";
      document.getElementById("adminLoginSection").style.display="none";
      document.getElementById("userLoginSection").style.display="none";
      loadProducts();
    })
    .catch(e=>alert("Admin Login failed: "+e.message));
}

window.logoutAdmin = function(){
  signOut(auth).then(()=>{
    document.getElementById("adminPanel").style.display="none";
    document.getElementById("adminLoginSection").style.display="block";
  });
}

// =================== Add Product (Admin) ===================
window.addProduct = async function(){
  const name = document.getElementById("pName").value;
  const price = document.getElementById("pPrice").value;
  const cat = document.getElementById("pCat").value;
  const imageFile = document.getElementById("pImage").files[0];
  if(!name || !price || !imageFile){ alert("Fill all fields"); return; }

  const storageRef = ref(storage, "products/"+Date.now()+"_"+imageFile.name);
  await uploadBytes(storageRef, imageFile);
  const url = await getDownloadURL(storageRef);

  await addDoc(collection(db, "products"), { name, price, cat, desc: name, image: url });
  loadProducts();
}

// =================== Delete Product (Admin) ===================
window.deleteProduct = async function(id){
  if(confirm("Are you sure to delete this product?")){
    await deleteDoc(doc(db, "products", id));
    loadProducts();
  }
}

// =================== Users Login/Register ===================
window.registerUser = function(){
  const email = document.getElementById("userEmail").value.trim();
  const pass = document.getElementById("userPassword").value.trim();
  if(!email || !pass){ alert("Fill all fields"); return; }

  createUserWithEmailAndPassword(auth, email, pass)
    .then(() => {
      alert("User Registered Successfully!");
      document.getElementById("userPanel").style.display="block";
      document.getElementById("userLoginSection").style.display="none";
      loadProducts();
    })
    .catch(e=>alert("Register failed: "+e.message));
}

window.loginUser = function(){
  const email = document.getElementById("userEmail").value.trim();
  const pass = document.getElementById("userPassword").value.trim();
  if(!email || !pass){ alert("Fill all fields"); return; }

  signInWithEmailAndPassword(auth, email, pass)
    .then(() => {
      document.getElementById("userPanel").style.display="block";
      document.getElementById("userLoginSection").style.display="none";
      loadProducts();
    })
    .catch(e=>alert("User Login failed: "+e.message));
}

window.logoutUser = function(){
  signOut(auth).then(()=>{
    document.getElementById("userPanel").style.display="none";
    document.getElementById("userLoginSection").style.display="block";
  });
}

// =================== Load Products ===================
window.loadProducts = async function(){
  const searchVal = document.getElementById("search") ? document.getElementById("search").value.toLowerCase() : "";
  const productsDiv = document.getElementById("products");
  productsDiv.innerHTML = "";

  const querySnapshot = await getDocs(collection(db, "products"));
  querySnapshot.forEach(doc=>{
    const p = doc.data();
    if(!searchVal || p.name.toLowerCase().includes(searchVal)){
      const card = document.createElement("div");
      card.className="card";
      card.innerHTML=`
        <img src="${p.image}">
        <h4>${p.name}</h4>
        <p>Rs. ${p.price}</p>
        <button onclick="addToCart('${p.name}',${p.price})">Add to Cart</button>
        <button style="background:red" onclick="deleteProduct('${doc.id}')">Delete</button>
      `;
      productsDiv.appendChild(card);
    }
  });
}

// =================== Cart & Checkout ===================
window.addToCart = function(name, price){
  cart.push({name, price});
  renderCart();
}

window.renderCart = function(){
  document.getElementById("cartList").innerText = cart.map(c=>c.name+" Rs."+c.price).join("\n");
}

window.checkout = function(){
  if(cart.length==0){alert("Cart empty"); return;}
  let msg = cart.map(c=>c.name+" Rs."+c.price).join("%0A");
  msg += "%0A%0APayment: "+document.getElementById("payment").value;
  window.open("https://wa.me/923000000000?text=Order%0A"+msg);
}

window.addEventListener("DOMContentLoaded", loadProducts);
</script>

<style>
body{margin:0;font-family:Arial,sans-serif;background:#f4f4f4}
header{background:#ff4500;color:white;padding:20px;text-align:center;font-size:28px}
.container{max-width:1200px;margin:auto;padding:15px}
input,select,button{padding:10px;border-radius:6px;border:1px solid #ccc;margin:5px 0}
button{background:#ff4500;color:white;border:none;cursor:pointer;transition:0.3s}
button:hover{background:#e03e00}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:15px}
.card{background:white;padding:15px;border-radius:10px;box-shadow:0 2px 8px rgba(0,0,0,0.1);transition:0.3s}
.card:hover{transform:scale(1.03)}
.card img{width:100%;height:150px;object-fit:cover;border-radius:8px}
#cartList{white-space:pre-line;background:#fff;padding:10px;border-radius:8px;box-shadow:0 1px 5px rgba(0,0,0,0.1)}
</style>
</head>
<body>

<header>Shopping Center 🛒</header>

<div class="container">

<!-- ADMIN LOGIN -->
<div id="adminLoginSection">
<h3>Admin Login</h3>
<input type="email" id="adminEmail" placeholder="Admin Email"><br>
<input type="password" id="adminPassword" placeholder="Password"><br>
<button onclick="loginAdmin()">Login as Admin</button>
</div>

<!-- ADMIN PANEL -->
<div id="adminPanel" style="display:none">
<h3>Admin Panel</h3>
<input type="text" id="pName" placeholder="Product Name"><br>
<input type="number" id="pPrice" placeholder="Price"><br>
<select id="pCat">
  <option>Men</option><option>Women</option><option>Accessories</option>
  <option>Electronics</option><option>Fitness</option>
</select><br>
<input type="file" id="pImage"><br>
<button onclick="addProduct()">Add Product</button>
<button onclick="logoutAdmin()">Logout</button>
<hr>
</div>

<!-- USER LOGIN/REGISTER -->
<div id="userLoginSection">
<h3>User Login / Register</h3>
<input type="email" id="userEmail" placeholder="Email"><br>
<input type="password" id="userPassword" placeholder="Password"><br>
<button onclick="loginUser()">Login</button>
<button onclick="registerUser()">Register</button>
</div>

<!-- USER PANEL -->
<div id="userPanel" style="display:none">
<h3>Welcome User</h3>
<button onclick="logoutUser()">Logout</button>
</div>

<!-- SEARCH -->
<input type="text" id="search" placeholder="Search products..." onkeyup="loadProducts()"><br>

<!-- PRODUCT LIST -->
<div class="products" id="products"></div>

<!-- CART -->
<h3>Your Cart</h3>
<div id="cartList"></div>
<select id="payment">
  <option>Cash on Delivery</option>
  <option>JazzCash</option>
  <option>EasyPaisa</option>
</select>
<button onclick="checkout()">Order via WhatsApp</button>

</div>
</body>
</html>
