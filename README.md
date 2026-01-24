<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body{margin:0;font-family:Arial;background:#f4f4f4}
header{background:#ff4500;color:#fff;padding:25px;text-align:center;font-size:28px;font-weight:bold;text-shadow:1px 1px #000}
.container{max-width:1400px;margin:auto;padding:20px}
.flex{display:flex;gap:10px;flex-wrap:wrap;margin-bottom:15px}
input,textarea,select,button{padding:10px;margin:5px 0;border-radius:6px;border:1px solid #ccc}
button{cursor:pointer;background:#25d366;color:#fff;font-weight:bold;transition:0.2s;border:none}
button:hover{opacity:0.9}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:20px}
.card{background:#fff;padding:15px;border-radius:12px;box-shadow:0 4px 12px rgba(0,0,0,0.15);transition:0.3s}
.card:hover{transform:scale(1.03)}
.card img{width:100%;height:180px;object-fit:cover;border-radius:10px}
.card h4{margin:10px 0 5px 0;font-size:18px;color:#333}
.card p{font-size:14px;color:#555;margin-bottom:10px}
.price{color:#e63946;font-weight:bold;font-size:17px;margin-bottom:10px}
.cart{background:#111;color:#fff;padding:15px;border-radius:10px;margin-top:20px}
footer{text-align:center;color:#555;padding:15px;margin-top:20px;font-size:14px}
</style>
</head>
<body>

<header>Shopping Center 🛒</header>
<div class="container">

<!-- ADMIN PANEL -->
<div class="flex">
<input id="pname" placeholder="Product Name">
<input id="pprice" placeholder="Price">
<input id="pimg" placeholder="Image URL">
<select id="pcat">
<option value="Men">Men</option>
<option value="Women">Women</option>
<option value="Accessories">Accessories</option>
<option value="Electronics">Electronics</option>
<option value="Fitness">Fitness</option>
</select>
</div>
<textarea id="pdesc" placeholder="Description"></textarea>
<button onclick="addProduct()">Add Product</button>

<!-- SEARCH & FILTER -->
<div class="flex">
<input id="search" placeholder="Search products..." onkeyup="renderProducts()">
<select id="filterCat" onchange="renderProducts()">
<option value="">All Categories</option>
<option value="Men">Men</option>
<option value="Women">Women</option>
<option value="Accessories">Accessories</option>
<option value="Electronics">Electronics</option>
<option value="Fitness">Fitness</option>
</select>
</div>

<!-- PRODUCTS -->
<div class="products" id="products"></div>

<!-- CART -->
<div class="cart">
<h3>Your Cart</h3>
<div id="cart"></div>
<select id="payment">
<option>Cash on Delivery</option>
<option>JazzCash</option>
<option>EasyPaisa</option>
</select>
<button onclick="checkout()">Place Order</button>
</div>

</div>

<footer>© 2026 Shopping Center | All rights reserved</footer>

<script>
// PROFESSIONAL PRODUCTS WITH IMAGES
let products=JSON.parse(localStorage.getItem("products"))||[
{name:"Men Casual Watch",price:2999,img:"https://images.unsplash.com/photo-1523275335684-37898b6baf30",desc:"Stylish casual watch for men.",cat:"Men"},
{name:"Wireless Bluetooth Headphones",price:4499,img:"https://images.unsplash.com/photo-1505740420928-5e560c06d30e",desc:"Noise reduction, long battery life.",cat:"Electronics"},
{name:"Women Leather Handbag",price:3899,img:"https://images.unsplash.com/photo-1584917865442-de89df76afd3",desc:"Elegant handbag for daily use.",cat:"Women"},
{name:"Running Shoes",price:5599,img:"https://images.unsplash.com/photo-1542291026-7eec264c27ff",desc:"Comfortable & durable sports shoes.",cat:"Men"},
{name:"Smart Fitness Band",price:2499,img:"https://images.unsplash.com/photo-1511707171634-5f897ff02aa9",desc:"Track steps, heart rate & sleep.",cat:"Fitness"},
{name:"Sunglasses",price:1999,img:"https://images.unsplash.com/photo-1511499767150-a48a237f0083",desc:"UV protection stylish sunglasses.",cat:"Accessories"},
{name:"Casual T-Shirt",price:1499,img:"https://images.unsplash.com/photo-1520975695543-431b42d1a3a7",desc:"Comfortable cotton t-shirt.",cat:"Men"},
{name:"Jeans Pants",price:2599,img:"https://images.unsplash.com/photo-1514996937319-344454492b37",desc:"Trendy denim jeans.",cat:"Men"},
{name:"Leather Wallet",price:1299,img:"https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f",desc:"Premium leather wallet.",cat:"Accessories"},
{name:"Sports Cap",price:799,img:"https://images.unsplash.com/photo-1520975919321-2b8f973b5e21",desc:"Stylish cap for outdoor.",cat:"Accessories"},
{name:"Smartphone Holder",price:699,img:"https://images.unsplash.com/photo-1599949810870-64d1595e4765",desc:"Phone holder for desk/car.",cat:"Electronics"},
{name:"Perfume Bottle",price:2199,img:"https://images.unsplash.com/photo-1560185127-6c54b37a1cde",desc:"Fragrance for men & women.",cat:"Accessories"},
{name:"Backpack",price:3299,img:"https://images.unsplash.com/photo-1503602642458-232111445657",desc:"Durable backpack for travel.",cat:"Accessories"},
{name:"Wireless Mouse",price:1099,img:"https://images.unsplash.com/photo-1587825140708-4e6b20f98f02",desc:"Smooth wireless mouse for PC.",cat:"Electronics"},
{name:"Laptop Sleeve",price:1899,img:"https://images.unsplash.com/photo-1555617117-08b7f1c5f9d6",desc:"Protect your laptop with style.",cat:"Electronics"},
{name:"Water Bottle",price:499,img:"https://images.unsplash.com/photo-1520975695543-431b42d1a3a7",desc:"Reusable water bottle.",cat:"Accessories"},
{name:"Headphone Stand",price:999,img:"https://images.unsplash.com/photo-1549924231-f129b911e442",desc:"Organize your headphones neatly.",cat:"Electronics"},
{name:"Desk Lamp",price:1399,img:"https://images.unsplash.com/photo-1512820790803-83ca734da794",desc:"LED desk lamp for study/work.",cat:"Electronics"},
{name:"Notebook Set",price:599,img:"https://images.unsplash.com/photo-1522202176988-66273c2fd55f",desc:"Set of 3 notebooks.",cat:"Accessories"},
{name:"Pen Set",price:299,img:"https://images.unsplash.com/photo-1510936111840-2c1e8b01e295",desc:"Colorful pen set for office.",cat:"Accessories"},
{name:"Women Sneakers",price:3999,img:"https://images.unsplash.com/photo-1600185360833-c9a62753f899",desc:"Comfortable sneakers for women.",cat:"Women"},
{name:"Men Formal Shoes",price:4999,img:"https://images.unsplash.com/photo-1580910051074-36ff97893ad9",desc:"Elegant formal shoes for men.",cat:"Men"},
{name:"Bluetooth Speaker",price:3299,img:"https://images.unsplash.com/photo-1581276879432-15b9f1c78d5a",desc:"Portable wireless speaker.",cat:"Electronics"},
{name:"Women Scarf",price:899,img:"https://images.unsplash.com/photo-1600185360807-38c1b0df063c",desc:"Stylish scarf for women.",cat:"Women"},
{name:"Fitness Yoga Mat",price:1299,img:"https://images.unsplash.com/photo-1584467735873-2d63f7e3a2ee",desc:"Non-slip yoga mat.",cat:"Fitness"},
{name:"Men Belt",price:699,img:"https://images.unsplash.com/photo-1560377701-607f4ed53b41",desc:"Premium leather belt.",cat:"Men"},
{name:"Women Earrings",price:1199,img:"https://images.unsplash.com/photo-1585386959984-a415522f28f7",desc:"Elegant earrings for women.",cat:"Women"}
];

let cart=JSON.parse(localStorage.getItem("cart"))||[];

function save(){localStorage.setItem("products",JSON.stringify(products)); localStorage.setItem("cart",JSON.stringify(cart));}

function addProduct(){ 
 let p={name:pname.value,price:parseInt(pprice.value),img:pimg.value,desc:pdesc.value,cat:pcat.value};
 products.push(p); pname.value=pprice.value=pimg.value=pdesc.value=""; renderProducts(); save();
}

function renderProducts(){
 let searchVal=search.value.toLowerCase(); 
 let catVal=filterCat.value;
 let filtered=products.filter(p=>p.name.toLowerCase().includes(searchVal)&&(catVal==""||p.cat==catVal));
 document.getElementById("products").innerHTML=filtered.map((p,i)=>`
 <div class="card">
  <img src="${p.img}">
  <h4>${p.name}</h4>
  <p>${p.desc}</p>
  <div class="price">Rs. ${p.price}</div>
  <button onclick="addCart(${i})">Add to Cart</button>
 </div>`).join("");
}

function addCart(i){cart.push(products[i]); renderCart(); save();}
function renderCart(){document.getElementById("cart").innerHTML=cart.map(c=>`${c.name} - Rs.${c.price}`).join("<br>");}
function checkout(){ 
 if(cart.length==0){alert("Cart is empty"); return;}
 let msg=cart.map(c=>c.name+" Rs."+c.price).join("%0A"); 
 let paymentMethod=document.getElementById("payment").value;
 msg+="%0A%0APayment Method: "+paymentMethod;
 window.open("https://wa.me/923000000000?text=Order%0A"+msg); 
 cart=[]; renderCart(); save();
}

renderProducts();
renderCart();
</script>
</body>
</html>
