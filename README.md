<html lang="en">
<head>
<meta charset="UTF-8">
<title>Shopping Center</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body{margin:0;font-family:Arial;background:#f5f5f5}
header{background:#ff4500;color:#fff;padding:25px;text-align:center;font-size:28px;font-weight:bold;text-shadow:1px 1px #000}
.container{max-width:1300px;margin:auto;padding:20px}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:20px}
.card{background:#fff;padding:15px;border-radius:12px;box-shadow:0 4px 12px rgba(0,0,0,0.15);transition:0.3s}
.card:hover{transform:scale(1.03)}
.card img{width:100%;height:180px;object-fit:cover;border-radius:10px}
.card h4{margin:10px 0 5px 0;font-size:18px;color:#333}
.card p{font-size:14px;color:#555;margin-bottom:10px}
.price{color:#e63946;font-weight:bold;font-size:17px;margin-bottom:10px}
button{background:#25d366;color:#fff;border:none;padding:10px;border-radius:6px;width:100%;cursor:pointer;font-weight:bold;transition:0.2s}
button:hover{opacity:0.9}
.cart{background:#111;color:#fff;padding:15px;border-radius:10px;margin-top:20px}
footer{text-align:center;color:#555;padding:15px;margin-top:20px;font-size:14px}
</style>
</head>
<body>

<header>Shopping Center 🛒</header>

<div class="container">

<div class="products" id="products"></div>

<div class="cart">
<h3>Your Cart</h3>
<div id="cart"></div>
<button onclick="checkout()">Order on WhatsApp</button>
</div>

</div>

<footer>© 2026 Shopping Center | Best Deals & Trusted Shop</footer>

<script>
let products=[
{name:"Men Casual Watch",price:2999,img:"https://images.unsplash.com/photo-1523275335684-37898b6baf30",desc:"Stylish casual watch for men."},
{name:"Wireless Bluetooth Headphones",price:4499,img:"https://images.unsplash.com/photo-1505740420928-5e560c06d30e",desc:"Noise reduction, long battery life."},
{name:"Women Leather Handbag",price:3899,img:"https://images.unsplash.com/photo-1584917865442-de89df76afd3",desc:"Elegant handbag for daily use."},
{name:"Running Shoes",price:5599,img:"https://images.unsplash.com/photo-1542291026-7eec264c27ff",desc:"Comfortable & durable sports shoes."},
{name:"Smart Fitness Band",price:2499,img:"https://images.unsplash.com/photo-1511707171634-5f897ff02aa9",desc:"Track steps, heart rate & sleep."},
{name:"Sunglasses",price:1999,img:"https://images.unsplash.com/photo-1511499767150-a48a237f0083",desc:"UV protection stylish sunglasses."},
{name:"Casual T-Shirt",price:1499,img:"https://images.unsplash.com/photo-1520975695543-431b42d1a3a7",desc:"Comfortable cotton t-shirt."},
{name:"Jeans Pants",price:2599,img:"https://images.unsplash.com/photo-1514996937319-344454492b37",desc:"Trendy denim jeans."},
{name:"Leather Wallet",price:1299,img:"https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f",desc:"Premium leather wallet."},
{name:"Sports Cap",price:799,img:"https://images.unsplash.com/photo-1520975919321-2b8f973b5e21",desc:"Stylish cap for outdoor."},
{name:"Smartphone Holder",price:699,img:"https://images.unsplash.com/photo-1599949810870-64d1595e4765",desc:"Phone holder for desk/car."},
{name:"Perfume Bottle",price:2199,img:"https://images.unsplash.com/photo-1560185127-6c54b37a1cde",desc:"Fragrance for men & women."},
{name:"Backpack",price:3299,img:"https://images.unsplash.com/photo-1503602642458-232111445657",desc:"Durable backpack for travel."},
{name:"Wireless Mouse",price:1099,img:"https://images.unsplash.com/photo-1587825140708-4e6b20f98f02",desc:"Smooth wireless mouse for PC."},
{name:"Laptop Sleeve",price:1899,img:"https://images.unsplash.com/photo-1555617117-08b7f1c5f9d6",desc:"Protect your laptop with style."},
{name:"Water Bottle",price:499,img:"https://images.unsplash.com/photo-1520975695543-431b42d1a3a7",desc:"Reusable water bottle."},
{name:"Headphone Stand",price:999,img:"https://images.unsplash.com/photo-1549924231-f129b911e442",desc:"Organize your headphones neatly."},
{name:"Desk Lamp",price:1399,img:"https://images.unsplash.com/photo-1512820790803-83ca734da794",desc:"LED desk lamp for study/work."},
{name:"Notebook Set",price:599,img:"https://images.unsplash.com/photo-1522202176988-66273c2fd55f",desc:"Set of 3 notebooks."},
{name:"Pen Set",price:299,img:"https://images.unsplash.com/photo-1510936111840-2c1e8b01e295",desc:"Colorful pen set for office."}
];

let cart=[];

function renderProducts(){
 document.getElementById("products").innerHTML=
 products.map((p,i)=>`
 <div class="card">
  <img src="${p.img}">
  <h4>${p.name}</h4>
  <p>${p.desc}</p>
  <div class="price">Rs. ${p.price}</div>
  <button onclick="addCart(${i})">Add to Cart</button>
 </div>`).join("");
}

function addCart(i){
 cart.push(products[i]);
 document.getElementById("cart").innerHTML=
 cart.map(c=>`${c.name} - Rs.${c.price}`).join("<br>");
}

function checkout(){
 let msg=cart.map(c=>c.name+" Rs."+c.price).join("%0A");
 window.open("https://wa.me/923000000000?text=Order%0A"+msg);
}

renderProducts();
</script>

</body>
</html>
