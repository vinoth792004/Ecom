<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Mini eCommerce Site</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
    }

    header {
      background-color: #333;
      color: white;
      padding: 1em;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    header h1 {
      margin: 0;
    }

    #cart-btn {
      background: #ff9900;
      color: white;
      border: none;
      padding: 10px 15px;
      font-size: 16px;
      cursor: pointer;
    }

    #product-list {
      display: flex;
      flex-wrap: wrap;
      gap: 1em;
      padding: 1em;
      justify-content: center;
    }

    .product {
      border: 1px solid #ccc;
      padding: 1em;
      width: 200px;
      text-align: center;
      background: #f9f9f9;
    }

    .product img {
      max-width: 100%;
      height: auto;
    }

    .product h3 {
      margin: 0.5em 0;
    }

    .product button {
      background: #28a745;
      color: white;
      border: none;
      padding: 8px 12px;
      cursor: pointer;
    }

    #cart-sidebar {
      position: fixed;
      top: 0;
      right: -320px;
      width: 300px;
      height: 100%;
      background: #fff;
      border-left: 1px solid #ccc;
      box-shadow: -2px 0 5px rgba(0, 0, 0, 0.2);
      padding: 1em;
      overflow-y: auto;
      transition: right 0.3s;
    }

    #cart-sidebar.open {
      right: 0;
    }

    #cart-sidebar h2 {
      margin-top: 0;
    }

    #cart-items li {
      margin: 0.5em 0;
    }

    #cart-sidebar button {
      background: #007bff;
      color: white;
      border: none;
      padding: 10px;
      margin-top: 1em;
      width: 100%;
      cursor: pointer;
    }
  </style>
</head>
<body>

  <header>
    <h1>My eShop</h1>
    <button id="cart-btn">🛒 Cart (<span id="cart-count">0</span>)</button>
  </header>

  <main id="product-list">
    <!-- Products will be injected by JavaScript -->
  </main>

  <aside id="cart-sidebar">
    <h2>Your Cart</h2>
    <ul id="cart-items"></ul>
    <p><strong>Total:</strong> $<span id="cart-total">0</span></p>
    <button onclick="checkout()">Checkout</button>
  </aside>

  <script>
    const products = [
      { id: 1, name: "T-Shirt", price: 20, image: "https://via.placeholder.com/200x150?text=T-Shirt" },
      { id: 2, name: "Sneakers", price: 50, image: "https://via.placeholder.com/200x150?text=Sneakers" },
      { id: 3, name: "Hat", price: 15, image: "https://via.placeholder.com/200x150?text=Hat" },
      { id: 4, name: "Backpack", price: 35, image: "https://via.placeholder.com/200x150?text=Backpack" }
    ];

    const cart = [];

    function renderProducts() {
      const productList = document.getElementById("product-list");
      products.forEach(product => {
        const div = document.createElement("div");
        div.className = "product";
        div.innerHTML = `
          <img src="${product.image}" alt="${product.name}">
          <h3>${product.name}</h3>
          <p>$${product.price}</p>
          <button onclick="addToCart(${product.id})">Add to Cart</button>
        `;
        productList.appendChild(div);
      });
    }

    function addToCart(productId) {
      const product = products.find(p => p.id === productId);
      cart.push(product);
      updateCart();
    }

    function updateCart() {
      const cartCount = document.getElementById("cart-count");
      const cartItems = document.getElementById("cart-items");
      const cartTotal = document.getElementById("cart-total");

      cartCount.textContent = cart.length;
      cartItems.innerHTML = "";

      let total = 0;
      cart.forEach(item => {
        const li = document.createElement("li");
        li.textContent = `${item.name} - $${item.price}`;
        cartItems.appendChild(li);
        total += item.price;
      });

      cartTotal.textContent = total.toFixed(2);
    }

    document.getElementById("cart-btn").addEventListener("click", () => {
      document.getElementById("cart-sidebar").classList.toggle("open");
    });

    function checkout() {
      alert("Thank you for your purchase! (This is a frontend demo)");
      cart.length = 0; // Clear cart
      updateCart();
      document.getElementById("cart-sidebar").classList.remove("open");
    }

    renderProducts();
  </script>

</body>
</html>
