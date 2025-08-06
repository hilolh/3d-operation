
      color: #01579b;
    }
    .order-section button {
      background-color: #0288d1;
      color: white;
      padding: 1rem 2rem;
      font-size: 1.2rem;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      margin-top: 1rem;
    }
    .order-section button:hover {
      background-color: #0277bd;
    }
    .recommended {
      background: white;
      padding: 1rem;
      border-radius: 8px;
      box-shadow: 0 0 5px #81d4fa;
      margin-top: 1rem;
    }
    .flavored-list {
      list-style: none;
      padding: 0;
    }
    .flavored-list li {
      background: white;
      margin-bottom: 10px;
      padding: 10px 15px;
      border-radius: 6px;
      box-shadow: 0 0 5px #81d4fa;
    }
    footer {
      text-align: center;
      padding: 1rem;
      background-color: #0288d1;
      color: white;
      margin-top: 3rem;
    }
    /* Simple form styling */
    form label {
      display: block;
      margin-top: 1rem;
      font-weight: 600;
    }
    form input, form select, form textarea {
      width: 100%;
      padding: 0.6rem;
      margin-top: 0.3rem;
      border-radius: 4px;
      border: 1px solid #0288d1;
      font-size: 1rem;
    }
    form button {
      margin-top: 1.5rem;
      background-color: #0288d1;
      color: white;
      border: none;
      padding: 1rem 2rem;
      border-radius: 6px;
      cursor: pointer;
      font-size: 1.1rem;
    }
    form button:hover {
      background-color: #0277bd;
    }
    .hidden {
      display: none;
    }
  </style>
</head>
<body>

<header>
  <div class="logo">Yosari<span class="droplet">💧</span></div>
  <nav>
    <a href="#home" onclick="showSection('home')">Home</a>
    <a href="#about" onclick="showSection('about')">About</a>
    <a href="#flavored" onclick="showSection('flavored')">Flavored Waters</a>
    <a href="#order" onclick="showSection('order')">Order</a>
  </nav>
</header>

<main>

  <section id="home" class="section">
    <h1>Welcome to Yosari</h1>
    <p>Your fresh water delivery service.</p>
    <div class="order-section">
      <button onclick="showSection('order')">Order Now 💧</button>
    </div>
    <h2>Recommended for You</h2>
    <div class="recommended">
      <p>Try our best-selling mineral water and flavored waters for a refreshing experience.</p>
    </div>
  </section>

  <section id="about" class="section hidden">
    <h2>About Yosari</h2>
    <p>You can order water from our company. We offer different kinds of water — from pure mineral water to flavored varieties — to keep you refreshed and hydrated.</p>
    <p>Our mission is to provide clean, fresh, and delicious water delivered right to your door.</p>
  </section>

  <section id="flavored" class="section hidden">
    <h2>Flavored Waters</h2>
    <ul class="flavored-list">
      <li> Lemon Mint — Refreshing lemon with a hint of mint.</li>
      <li> Berry Blast — Mixed berries flavor for a sweet twist.</li>
      <li> Cucumber Lime — Cool cucumber with zesty lime.</li>
      <li> Tropical Mango — Sweet mango with tropical vibes.</li>
    </ul>
  </section>

  <section id="order" class="section hidden">
    <h2>Order Water</h2>
    <form id="orderForm" onsubmit="submitOrder(event)">
      <label for="waterType">Select Water Type:</label>
      <select id="waterType" name="waterType" required>
        <option value="" disabled selected>Select an option</option>
        <option value="Mineral Water">Mineral Water</option>
        <option value="Lemon Mint">Lemon Mint (Flavored)</option>
        <option value="Berry Blast">Berry Blast (Flavored)</option>
        <option value="Cucumber Lime">Cucumber Lime (Flavored)</option>
        <option value="Tropical Mango">Tropical Mango (Flavored)</option>
      </select>

      <label for="quantity">Quantity (bottles):</label>
      <input type="number" id="quantity" name="quantity" min="1" required />

      <label for="address">Delivery Address:</label>
      <textarea id="address" name="address" rows="3" placeholder="Enter your full delivery address" required></textarea>

      <label for="contact">Contact Phone or WhatsApp:</label>
      <input type="tel" id="contact" name="contact" placeholder="+256..." required />

      <button type="submit">Submit Order</button>
    </form>
    <p id="confirmation" style="color: green; font-weight: 600; margin-top: 1rem;"></p>
  </section>

</main>

<footer>
  &copy; 2025 Yosari Water Delivery. All rights reserved.
</footer>

<script>
  function showSection(id) {
    document.querySelectorAll('.section').forEach(section => {
      section.classList.add('hidden');
    });
    document.getElementById(id).classList.remove('hidden');
    window.location.hash = id;
  }

  // Show home section by default
  if (!window.location.hash) {
    showSection('home');
  } else {
    const hash = window.location.hash.substring(1);
    if(document.getElementById(hash)) {
      showSection(hash);
    } else {
      showSection('home');
    }
  }

  function submitOrder(event) {
    event.preventDefault();
    const waterType = document.getElementById('waterType').value;
    const quantity = document.getElementById('quantity').value;
    const address = document.getElementById('address').value;
    const contact = document.getElementById('contact').value;

    // For now just show confirmation and open WhatsApp with pre-filled message
    const message = 
      `Hello, I would like to order ${quantity} bottle(s) of ${waterType}.\n` +
      `Delivery Address: ${address}\n` +
      `Contact: ${contact}`;

    const encodedMessage = encodeURIComponent(message);
    const whatsappUrl = `https://wa.me/${contact.replace(/\D/g,'')}?text=${encodedMessage}`;

    document.getElementById('confirmation').textContent = 'Thank you for your order! We will contact you shortly.';
    window.open(whatsappUrl, '_blank');
    event.target.reset();
  }
</script>

</body>
</html>
