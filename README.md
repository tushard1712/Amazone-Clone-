# Amazone-Clone-
Developed an Amazon-inspired e-commerce website clone using HTML, CSS, and JavaScript, featuring product listings, responsive UI, and a structured layout similar to the original platform.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Amazon Clone - Online Shopping</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            background-color: #eaeded;
        }

        .navbar {
            background-color: #131921;
            color: white;
            padding: 10px 20px;
            display: flex;
            align-items: center;
            gap: 20px;
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .logo {
            font-size: 24px;
            font-weight: bold;
            cursor: pointer;
            background: linear-gradient(to bottom, #ffa500, #ff6600);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .search-bar {
            flex: 1;
            display: flex;
        }

        .search-bar input {
            flex: 1;
            padding: 10px;
            border: none;
            outline: none;
            border-radius: 4px 0 0 4px;
        }

        .search-bar button {
            padding: 10px 20px;
            background-color: #febd69;
            border: none;
            cursor: pointer;
            border-radius: 0 4px 4px 0;
            font-weight: bold;
        }

        .nav-links {
            display: flex;
            gap: 20px;
            align-items: center;
        }

        .nav-item {
            cursor: pointer;
            padding: 5px 10px;
            border: 1px solid transparent;
            border-radius: 2px;
            transition: border-color 0.2s;
        }

        .nav-item:hover {
            border-color: white;
        }

        .cart-icon {
            position: relative;
            font-size: 24px;
        }

        .cart-count {
            position: absolute;
            top: -8px;
            right: -8px;
            background-color: #ff6600;
            color: white;
            border-radius: 50%;
            padding: 2px 6px;
            font-size: 12px;
            font-weight: bold;
        }


        .sub-navbar {
            background-color: #232f3e;
            color: white;
            padding: 10px 20px;
            display: flex;
            gap: 20px;
            overflow-x: auto;
        }

        .sub-navbar a {
            color: white;
            text-decoration: none;
            white-space: nowrap;
            padding: 5px 10px;
            border-radius: 2px;
            transition: background-color 0.2s;
        }

        .sub-navbar a:hover {
            background-color: #374151;
        }


        .hero {
            background: linear-gradient(to bottom, #232f3e, transparent);
            height: 400px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 32px;
            font-weight: bold;
            position: relative;
            overflow: hidden;
        }

        .hero-image {
            position: absolute;
            width: 100%;
            height: 100%;
            object-fit: cover;
            opacity: 0.3;
        }

        .hero-text {
            position: relative;
            z-index: 1;
            text-align: center;
        }


        .filter-section {
            background-color: white;
            padding: 20px;
            margin: 20px;
            border-radius: 8px;
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            align-items: center;
        }

        .filter-section select, .filter-section input {
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            outline: none;
        }

        .filter-section button {
            padding: 10px 20px;
            background-color: #ff6600;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
        }

        .filter-section button:hover {
            background-color: #e55d00;
        }

        /* Products Grid */
        .products-container {
            padding: 20px;
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
            max-width: 1400px;
            margin: 0 auto;
        }

        .product-card {
            background-color: white;
            border-radius: 8px;
            padding: 15px;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
            display: flex;
            flex-direction: column;
        }

        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }

        .product-image {
            width: 100%;
            height: 250px;
            object-fit: contain;
            margin-bottom: 15px;
        }

        .product-title {
            font-size: 16px;
            font-weight: 600;
            margin-bottom: 10px;
            height: 48px;
            overflow: hidden;
            text-overflow: ellipsis;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
        }

        .product-rating {
            color: #ffa41c;
            margin-bottom: 10px;
        }

        .product-price {
            font-size: 24px;
            font-weight: bold;
            color: #B12704;
            margin-bottom: 10px;
        }

        .product-prime {
            color: #007185;
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 15px;
        }

        .add-to-cart-btn {
            background-color: #ffd814;
            border: none;
            padding: 10px;
            border-radius: 20px;
            cursor: pointer;
            font-weight: bold;
            transition: background-color 0.2s;
            margin-top: auto;
        }

        .add-to-cart-btn:hover {
            background-color: #f7ca00;
        }

        /* Cart Sidebar */
        .cart-sidebar {
            position: fixed;
            right: -400px;
            top: 0;
            width: 400px;
            height: 100%;
            background-color: white;
            box-shadow: -2px 0 10px rgba(0,0,0,0.2);
            transition: right 0.3s;
            z-index: 2000;
            display: flex;
            flex-direction: column;
        }

        .cart-sidebar.active {
            right: 0;
        }

        .cart-header {
            background-color: #232f3e;
            color: white;
            padding: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .close-cart {
            cursor: pointer;
            font-size: 24px;
        }

        .cart-items {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
        }

        .cart-item {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
            padding-bottom: 20px;
            border-bottom: 1px solid #ddd;
        }

        .cart-item-image {
            width: 80px;
            height: 80px;
            object-fit: contain;
        }

        .cart-item-details {
            flex: 1;
        }

        .cart-item-title {
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 5px;
        }

        .cart-item-price {
            color: #B12704;
            font-weight: bold;
            margin-bottom: 10px;
        }

        .quantity-controls {
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .qty-btn {
            padding: 5px 10px;
            background-color: #f0f0f0;
            border: 1px solid #ddd;
            cursor: pointer;
            border-radius: 4px;
        }

        .remove-btn {
            color: #007185;
            cursor: pointer;
            font-size: 12px;
            margin-top: 5px;
        }

        .cart-footer {
            padding: 20px;
            border-top: 1px solid #ddd;
            background-color: #f8f8f8;
        }

        .cart-total {
            font-size: 20px;
            font-weight: bold;
            margin-bottom: 15px;
        }

        .checkout-btn {
            width: 100%;
            padding: 15px;
            background-color: #ffd814;
            border: none;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            font-size: 16px;
        }

        .checkout-btn:hover {
            background-color: #f7ca00;
        }

        .empty-cart {
            text-align: center;
            padding: 40px;
            color: #666;
        }

        /* Toast Notification */
        .toast {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: #232f3e;
            color: white;
            padding: 15px 25px;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.3s;
            z-index: 3000;
        }

        .toast.show {
            opacity: 1;
            transform: translateY(0);
        }

        /* Responsive */
        @media (max-width: 768px) {
            .navbar {
                flex-wrap: wrap;
            }
            
            .search-bar {
                order: 3;
                width: 100%;
                margin-top: 10px;
            }

            .products-container {
                grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
                gap: 10px;
                padding: 10px;
            }

            .cart-sidebar {
                width: 100%;
                right: -100%;
            }

            .hero {
                height: 250px;
                font-size: 24px;
            }
        }
    </style>
</head>
<body>

    <div class="navbar">
        <div class="logo">amazon</div>
        <div class="search-bar">
            <input type="text" placeholder="Search products..." id="searchInput">
            <button onclick="searchProducts()">🔍</button>
        </div>
        <div class="nav-links">
            <div class="nav-item">Hello, Sign in</div>
            <div class="nav-item">Returns & Orders</div>
            <div class="nav-item cart-icon" onclick="toggleCart()">
                🛒
                <span class="cart-count" id="cartCount">0</span>
            </div>
        </div>
    </div>


    <div class="sub-navbar">
        <a href="#" onclick="filterByCategory('all')">All</a>
        <a href="#" onclick="filterByCategory('Electronics')">Electronics</a>
        <a href="#" onclick="filterByCategory('Fashion')">Fashion</a>
        <a href="#" onclick="filterByCategory('Home')">Home & Kitchen</a>
        <a href="#" onclick="filterByCategory('Books')">Books</a>
        <a href="#" onclick="filterByCategory('Sports')">Sports</a>
        <a href="#" onclick="filterByCategory('Toys')">Toys</a>
    </div>


    <div class="hero">
        <div class="hero-text">Shop Great Deals Today!</div>
    </div>


    <div class="filter-section">
        <select id="sortSelect" onchange="sortProducts()">
            <option value="">Sort By</option>
            <option value="price-low">Price: Low to High</option>
            <option value="price-high">Price: High to Low</option>
            <option value="rating">Customer Rating</option>
        </select>
        <select id="priceFilter" onchange="filterByPrice()">
            <option value="">All Prices</option>
            <option value="0-50">Under $50</option>
            <option value="50-100">$50 - $100</option>
            <option value="100-500">$100 - $500</option>
            <option value="500+">$500 & Above</option>
        </select>
        <button onclick="clearFilters()">Clear Filters</button>
    </div>
    <div class="products-container" id="productsContainer"></div>


    <div class="cart-sidebar" id="cartSidebar">
        <div class="cart-header">
            <h2>Shopping Cart</h2>
            <span class="close-cart" onclick="toggleCart()">✕</span>
        </div>
        <div class="cart-items" id="cartItems"></div>
        <div class="cart-footer">
            <div class="cart-total">Total: $<span id="cartTotal">0.00</span></div>
            <button class="checkout-btn" onclick="checkout()">Proceed to Checkout</button>
        </div>
    </div>


    <div class="toast" id="toast"></div>

    <script>

        const allProducts = [
            { id: 1, name: 'Wireless Bluetooth Headphones', category: 'Electronics', price: 79.99, rating: 4.5, image: 'https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=400', prime: true },
            { id: 2, name: 'Smart Watch Fitness Tracker', category: 'Electronics', price: 149.99, rating: 4.3, image: 'https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=400', prime: true },
            { id: 3, name: 'Cotton T-Shirt Pack of 3', category: 'Fashion', price: 29.99, rating: 4.6, image: 'https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?w=400', prime: false },
            { id: 4, name: 'Running Shoes for Men', category: 'Fashion', price: 89.99, rating: 4.4, image: 'https://images.unsplash.com/photo-1542291026-7eec264c27ff?w=400', prime: true },
            { id: 5, name: 'Stainless Steel Coffee Maker', category: 'Home', price: 59.99, rating: 4.7, image: 'https://images.unsplash.com/photo-1517668808822-9ebb02f2a0e6?w=400', prime: true },
            { id: 6, name: 'Non-Stick Cookware Set', category: 'Home', price: 129.99, rating: 4.5, image: 'https://images.unsplash.com/photo-1556910103-1c02745aae4d?w=400', prime: false },
            { id: 7, name: 'Best Selling Novel - Hardcover', category: 'Books', price: 24.99, rating: 4.8, image: 'https://images.unsplash.com/photo-1544947950-fa07a98d237f?w=400', prime: true },
            { id: 8, name: 'Yoga Mat with Carry Strap', category: 'Sports', price: 34.99, rating: 4.6, image: 'https://images.unsplash.com/photo-1601925260368-ae2f83cf8b7f?w=400', prime: false },
            { id: 9, name: 'Wireless Gaming Mouse', category: 'Electronics', price: 49.99, rating: 4.4, image: 'https://images.unsplash.com/photo-1527814050087-3793815479db?w=400', prime: true },
            { id: 10, name: 'LED Desk Lamp with USB Port', category: 'Home', price: 39.99, rating: 4.3, image: 'https://images.unsplash.com/photo-1507473885765-e6ed057f782c?w=400', prime: true },
            { id: 11, name: 'Denim Jeans - Slim Fit', category: 'Fashion', price: 54.99, rating: 4.5, image: 'https://images.unsplash.com/photo-1542272604-787c3835535d?w=400', prime: false },
            { id: 12, name: 'Building Blocks Set - 500 Pieces', category: 'Toys', price: 44.99, rating: 4.9, image: 'https://images.unsplash.com/photo-1587654780291-39c9404d746b?w=400', prime: true },
        ];

        let displayedProducts = [...allProducts];
        let cart = JSON.parse(localStorage.getItem('amazonCart')) || [];


        function init() {
            displayProducts(displayedProducts);
            updateCartUI();
        }


        function displayProducts(products) {
            const container = document.getElementById('productsContainer');
            container.innerHTML = products.map(product => `
                <div class="product-card">
                    <img src="${product.image}" alt="${product.name}" class="product-image">
                    <div class="product-title">${product.name}</div>
                    <div class="product-rating">${'⭐'.repeat(Math.floor(product.rating))} ${product.rating}</div>
                    <div class="product-price">$${product.price.toFixed(2)}</div>
                    ${product.prime ? '<div class="product-prime">✓ Prime FREE Delivery</div>' : ''}
                    <button class="add-to-cart-btn" onclick="addToCart(${product.id})">Add to Cart</button>
                </div>
            `).join('');
        }


        function addToCart(productId) {
            const product = allProducts.find(p => p.id === productId);
            const existingItem = cart.find(item => item.id === productId);

            if (existingItem) {
                existingItem.quantity++;
            } else {
                cart.push({ ...product, quantity: 1 });
            }

            saveCart();
            updateCartUI();
            showToast('Added to cart!');
        }


        function updateCartUI() {
            const cartCount = document.getElementById('cartCount');
            const cartItems = document.getElementById('cartItems');
            const cartTotal = document.getElementById('cartTotal');

            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            cartCount.textContent = totalItems;

            if (cart.length === 0) {
                cartItems.innerHTML = '<div class="empty-cart">Your cart is empty</div>';
                cartTotal.textContent = '0.00';
                return;
            }

            cartItems.innerHTML = cart.map(item => `
                <div class="cart-item">
                    <img src="${item.image}" alt="${item.name}" class="cart-item-image">
                    <div class="cart-item-details">
                        <div class="cart-item-title">${item.name}</div>
                        <div class="cart-item-price">$${item.price.toFixed(2)}</div>
                        <div class="quantity-controls">
                            <button class="qty-btn" onclick="updateQuantity(${item.id}, -1)">-</button>
                            <span>${item.quantity}</span>
                            <button class="qty-btn" onclick="updateQuantity(${item.id}, 1)">+</button>
                        </div>
                        <div class="remove-btn" onclick="removeFromCart(${item.id})">Remove</div>
                    </div>
                </div>
            `).join('');

            const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            cartTotal.textContent = total.toFixed(2);
        }


        function updateQuantity(productId, change) {
            const item = cart.find(item => item.id === productId);
            if (item) {
                item.quantity += change;
                if (item.quantity <= 0) {
                    removeFromCart(productId);
                } else {
                    saveCart();
                    updateCartUI();
                }
            }
        }


        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            saveCart();
            updateCartUI();
            showToast('Removed from cart');
        }


        function toggleCart() {
            document.getElementById('cartSidebar').classList.toggle('active');
        }


        function searchProducts() {
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            displayedProducts = allProducts.filter(product => 
                product.name.toLowerCase().includes(searchTerm) ||
                product.category.toLowerCase().includes(searchTerm)
            );
            displayProducts(displayedProducts);
        }


        function filterByCategory(category) {
            if (category === 'all') {
                displayedProducts = [...allProducts];
            } else {
                displayedProducts = allProducts.filter(p => p.category === category);
            }
            displayProducts(displayedProducts);
        }


        function sortProducts() {
            const sortValue = document.getElementById('sortSelect').value;
            
            switch(sortValue) {
                case 'price-low':
                    displayedProducts.sort((a, b) => a.price - b.price);
                    break;
                case 'price-high':
                    displayedProducts.sort((a, b) => b.price - a.price);
                    break;
                case 'rating':
                    displayedProducts.sort((a, b) => b.rating - a.rating);
                    break;
            }
            displayProducts(displayedProducts);
        }


        function filterByPrice() {
            const priceRange = document.getElementById('priceFilter').value;
            
            if (!priceRange) {
                displayedProducts = [...allProducts];
            } else if (priceRange === '500+') {
                displayedProducts = allProducts.filter(p => p.price >= 500);
            } else {
                const [min, max] = priceRange.split('-').map(Number);
                displayedProducts = allProducts.filter(p => p.price >= min && p.price <= max);
            }
            displayProducts(displayedProducts);
        }


        function clearFilters() {
            document.getElementById('sortSelect').value = '';
            document.getElementById('priceFilter').value = '';
            document.getElementById('searchInput').value = '';
            displayedProducts = [...allProducts];
            displayProducts(displayedProducts);
        }


        function checkout() {
            if (cart.length === 0) {
                showToast('Cart is empty!');
                return;
            }
            showToast('Proceeding to checkout...');
            setTimeout(() => {
                alert('Thank you for shopping! Order total: $' + cart.reduce((sum, item) => sum + (item.price * item.quantity), 0).toFixed(2));
                cart = [];
                saveCart();
                updateCartUI();
                toggleCart();
            }, 1000);
        }

        
        function saveCart() {
            localStorage.setItem('amazonCart', JSON.stringify(cart));
        }


        function showToast(message) {
            const toast = document.getElementById('toast');
            toast.textContent = message;
            toast.classList.add('show');
            setTimeout(() => {
                toast.classList.remove('show');
            }, 2000);
        }

       
        init();
    </script>
</body>
</html>–
