<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ShopCenter - Online Store</title>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; font-family: Arial, sans-serif; }
body { background: #f4f4f4; }

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background: #2c3e50;
  color: white;
}
header nav a { color: white; margin-left: 15px; text-decoration: none; }
header nav a:hover { text-decoration: underline; }

.hero {
  text-align: center;
  padding: 100px 20px;
  background: url('https://images.unsplash.com/photo-1511732358875-fcdc9f169d60?auto=format&fit=crop&w=1200&q=80') no-repeat center center/cover;
  color: white;
}
.hero button {
  margin-top: 20px;
  padding: 10px 25px;
  background: #e67e22;
  border: none;
  color: white;
  cursor: pointer;
  font-size: 16px;
}
.hero button:hover { background: #d35400; }

.products { padding: 50px 20px; text-align: center; }
.products h2 { margin-bottom: 30px; }
.product-grid { display: flex; justify-content: center; gap: 30px; flex-wrap: wrap; }
.product {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  width: 250px;
  transition: transform 0.2s;
}
.product:hover { transform: translateY(-5px); }
.product img { width: 100%; border-radius: 8px; }
.product h3 { margin-top: 10px; font-size: 18px; }
.product p { margin: 5px 0; font-weight: bold; }
.product button {
  margin-top: 10px;
  padding: 8px 15px;
  background: #3498db;
  border: none;
  color: white;
  cursor: pointer;
}
.product button:hover { background: #2980b9; }

footer { text-align: center; padding: 20px; background: #2c3e50; color: white; margin-top: 50px; }
</style>
</head>
<body>

<header>
  <div class="logo">ShopCenter</div>
  <nav>
    <a href="#">Home</a>
    <a href="#">Products</a>
    <a href="#">Contact</a>
  </nav>
</header>

<section class="hero">
  <h1>Welcome to ShopCenter</h1>
  <p>Discover Great Products Online!</p>
  <button>Shop Now</button>
</section>

<section class="products">
  <h2>Featured Products</h2>
  <div class="product-grid">

    <div class="product">
      <img src="https://images.unsplash.com/photo-1585386959984-a4155223cc27?auto=format&fit=crop&w=300&q=80" alt="Wireless Headphones">
      <h3>Wireless Headphones</h3>
      <p>$29.99</p>
      <button>Add to Cart</button>
    </div>

    <div class="product">
      <img src="https://images.unsplash.com/photo-1523275335684-37898b6baf30?auto=format&fit=crop&w=300&q=80" alt="Sport Sneakers">
      <h3>Sport Sneakers</h3>
      <p>$49.99</p>
      <button>Add to Cart</button>
    </div>

    <div class="product">
      <img src="https://images.unsplash.com/photo-1593032457865-d91aa8fd0bb1?auto=format&fit=crop&w=300&q=80" alt="Stylish Backpack">
      <h3>Stylish Backpack</h3>
      <p>$39.99</p>
      <button>Add to Cart</button>
    </div>

    <div class="product">
      <img src="https://images.unsplash.com/photo-1505740420928-5e560c06d30e?auto=format&fit=crop&w=300&q=80" alt="Smart Watch">
      <h3>Smart Watch</h3>
      <p>$59.99</p>
      <button>Add to Cart</button>
    </div>

    <div class="product">
      <img src="https://images.unsplash.com/photo-1618354692004-c7ff5e23e4d7?auto=format&fit=crop&w=300&q=80" alt="T-Shirt">
      <h3>Trendy T-Shirt</h3>
      <p>$19.99</p>
      <button>Add to Cart</button>
    </div>

    <div class="product">
      <img src="https://images.unsplash.com/photo-1600180758895-bb5b71c93c6b?auto=format&fit=crop&w=300&q=80" alt="Beauty Products">
      <h3>Beauty Kit</h3>
      <p>$34.99</p>
      <button>Add to Cart</button>
    </div>

    <div class="product">
      <img src="https://images.unsplash.com/photo-1606813901230-0c57c5d2f8d6?auto=format&fit=crop&w=300&q=80" alt="Sunglasses">
      <h3>Stylish Sunglasses</h3>
      <p>$24.99</p>
      <button>Add to Cart</button>
    </div>

    <div class="product">
      <img src="https://images.unsplash.com/photo-1603786509342-1c5d6b4dc6f3?auto=format&fit=crop&w=300&q=80" alt="Gadget">
      <h3>Smart Gadget</h3>
      <p>$79.99</p>
      <button>Add to Cart</button>
    </div>

  </div>
</section>

<footer>
  <p>&copy; 2026 ShopCenter</p>
</footer>

<script>
const buttons = document.querySelectorAll('.product button');
buttons.forEach(btn => {
  btn.addEventListener('click', () => {
    alert('Item added to cart!');
  });
});
</script>

</body>
</html>
