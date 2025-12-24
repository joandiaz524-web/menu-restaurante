<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Menú Digital | Pedidos por WhatsApp</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.3/build/qrcode.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        :root {
            --primary-color: #25D366;
            --secondary-color: #075E54;
            --accent-color: #128C7E;
            --light-color: #f8f9fa;
            --dark-color: #333;
            --gray-color: #6c757d;
            --border-radius: 12px;
            --box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        body {
            background-color: #f5f5f5;
            color: var(--dark-color);
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            background: linear-gradient(135deg, var(--secondary-color), var(--accent-color));
            color: white;
            border-radius: var(--border-radius);
            padding: 25px;
            margin-bottom: 30px;
            text-align: center;
            box-shadow: var(--box-shadow);
        }

        header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }

        header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }

        .whatsapp-icon {
            color: var(--primary-color);
            margin-right: 10px;
        }

        .restaurant-info {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
            background-color: white;
            border-radius: var(--border-radius);
            padding: 20px;
            margin-bottom: 30px;
            box-shadow: var(--box-shadow);
        }

        .contact-info {
            flex: 1;
            min-width: 300px;
        }

        .contact-info h3 {
            color: var(--secondary-color);
            margin-bottom: 15px;
        }

        .contact-info p {
            margin-bottom: 10px;
            display: flex;
            align-items: center;
        }

        .contact-info i {
            width: 25px;
            color: var(--accent-color);
        }

        .qr-section {
            text-align: center;
            padding: 15px;
        }

        #qrCode {
            width: 180px;
            height: 180px;
            margin: 0 auto 15px;
            background-color: white;
            padding: 10px;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
        }

        .qr-section p {
            font-size: 0.9rem;
            color: var(--gray-color);
        }

        .menu-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 25px;
            margin-bottom: 40px;
        }

        .category {
            background-color: white;
            border-radius: var(--border-radius);
            padding: 25px;
            box-shadow: var(--box-shadow);
        }

        .category h2 {
            color: var(--secondary-color);
            padding-bottom: 10px;
            margin-bottom: 20px;
            border-bottom: 3px solid var(--primary-color);
            display: flex;
            align-items: center;
        }

        .category h2 i {
            margin-right: 10px;
        }

        .menu-item {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 1px dashed #eee;
        }

        .item-info {
            flex: 1;
        }

        .item-info h3 {
            font-size: 1.2rem;
            margin-bottom: 5px;
            color: var(--dark-color);
        }

        .item-info p {
            color: var(--gray-color);
            font-size: 0.95rem;
            margin-bottom: 10px;
        }

        .item-price {
            font-weight: bold;
            color: var(--accent-color);
            font-size: 1.3rem;
        }

        .item-controls {
            display: flex;
            align-items: center;
            margin-top: 10px;
        }

        .quantity-btn {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            border: none;
            background-color: var(--accent-color);
            color: white;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .quantity-display {
            margin: 0 15px;
            font-weight: bold;
            min-width: 30px;
            text-align: center;
        }

        .cart-container {
            background-color: white;
            border-radius: var(--border-radius);
            padding: 25px;
            box-shadow: var(--box-shadow);
            margin-bottom: 30px;
            position: sticky;
            top: 20px;
        }

        .cart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--primary-color);
        }

        .cart-header h2 {
            color: var(--secondary-color);
            display: flex;
            align-items: center;
        }

        .cart-header i {
            margin-right: 10px;
        }

        #clearCart {
            background-color: #ff6b6b;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.9rem;
        }

        #cartItems {
            max-height: 300px;
            overflow-y: auto;
            margin-bottom: 20px;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid #eee;
        }

        .cart-item-name {
            flex: 1;
        }

        .cart-item-quantity {
            margin: 0 15px;
            font-weight: bold;
        }

        .cart-item-price {
            font-weight: bold;
            color: var(--accent-color);
        }

        .cart-total {
            display: flex;
            justify-content: space-between;
            font-size: 1.3rem;
            font-weight: bold;
            padding-top: 15px;
            border-top: 2px solid var(--primary-color);
        }

        .cart-actions {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-top: 25px;
        }

        #sendOrder {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 16px;
            border-radius: var(--border-radius);
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: background-color 0.3s;
        }

        #sendOrder:hover {
            background-color: var(--secondary-color);
        }

        #sendOrder i {
            margin-right: 10px;
            font-size: 1.3rem;
        }

        .instructions {
            background-color: #e8f5e9;
            border-radius: var(--border-radius);
            padding: 20px;
            margin-top: 30px;
            border-left: 5px solid var(--primary-color);
        }

        .instructions h3 {
            color: var(--secondary-color);
            margin-bottom: 10px;
            display: flex;
            align-items: center;
        }

        .instructions h3 i {
            margin-right: 10px;
        }

        .instructions ol {
            margin-left: 20px;
        }

        .instructions li {
            margin-bottom: 8px;
        }

        footer {
            text-align: center;
            padding: 20px;
            color: var(--gray-color);
            font-size: 0.9rem;
            border-top: 1px solid #ddd;
            margin-top: 40px;
        }

        @media (max-width: 768px) {
            .restaurant-info {
                flex-direction: column;
                text-align: center;
            }

            .contact-info p {
                justify-content: center;
            }

            .menu-container {
                grid-template-columns: 1fr;
            }

            header h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fab fa-whatsapp whatsapp-icon"></i> Menú Digital</h1>
            <p>Explora nuestro menú y envía tu pedido directamente por WhatsApp</p>
        </header>

        <div class="restaurant-info">
            <div class="contact-info">
                <h3>Restaurante "Sabor a Casa"</h3>
                <p><i class="fas fa-map-marker-alt"></i> Av. Principal 123, Ciudad</p>
                <p><i class="fas fa-phone"></i> Teléfono: +1 234 567 890</p>
                <p><i class="fas fa-clock"></i> Horario: 9:00 AM - 10:00 PM</p>
                <p><i class="fab fa-whatsapp"></i> WhatsApp: +1 234 567 890</p>
            </div>
            
            <div class="qr-section">
                <div id="qrCode"></div>
                <p>Escanea para acceder al menú</p>
            </div>
        </div>

        <div class="menu-container">
            <!-- Categoría Entradas -->
            <div class="category">
                <h2><i class="fas fa-utensils"></i> Entradas</h2>
                
                <div class="menu-item">
                    <div class="item-info">
                        <h3>Sopa del Día</h3>
                        <p>Sopa cremosa preparada con ingredientes frescos del día.</p>
                        <div class="item-controls">
                            <button class="quantity-btn minus" data-item="Sopa del Día" data-price="5.99">-</button>
                            <span class="quantity-display" id="qty-Sopa del Día">0</span>
                            <button class="quantity-btn plus" data-item="Sopa del Día" data-price="5.99">+</button>
                        </div>
                    </div>
                    <div class="item-price">$5.99</div>
                </div>
                
                <div class="menu-item">
                    <div class="item-info">
                        <h3>Ensalada César</h3>
                        <p>Lechuga romana, croutons, queso parmesano y aderezo césar.</p>
                        <div class="item-controls">
                            <button class="quantity-btn minus" data-item="Ensalada César" data-price="7.50">-</button>
                            <span class="quantity-display" id="qty-Ensalada César">0</span>
                            <button class="quantity-btn plus" data-item="Ensalada César" data-price="7.50">+</button>
                        </div>
                    </div>
                    <div class="item-price">$7.50</div>
                </div>
                
                <div class="menu-item">
                    <div class="item-info">
                        <h3>Nachos con Queso</h3>
                        <p>Tortilla chips con queso fundido, guacamole y pico de gallo.</p>
                        <div class="item-controls">
                            <button class="quantity-btn minus" data-item="Nachos con Queso" data-price="8.99">-</button>
                            <span class="quantity-display" id="qty-Nachos con Queso">0</span>
                            <button class="quantity-btn plus" data-item="Nachos con Queso" data-price="8.99">+</button>
                        </div>
                    </div>
                    <div class="item-price">$8.99</div>
                </div>
            </div>
            
            <!-- Categoría Platos Principales -->
            <div class="category">
                <h2><i class="fas fa-hamburger"></i> Platos Principales</h2>
                
                <div class="menu-item">
                    <div class="item-info">
                        <h3>Pasta Alfredo</h3>
                        <p>Pasta fetuccini con salsa alfredo cremosa y pollo a la parrilla.</p>
                        <div class="item-controls">
                            <button class="quantity-btn minus" data-item="Pasta Alfredo" data-price="12.99">-</button>
                            <span class="quantity-display" id="qty-Pasta Alfredo">0</span>
                            <button class="quantity-btn plus" data-item="Pasta Alfredo" data-price="12.99">+</button>
                        </div>
                    </div>
                    <div class="item-price">$12.99</div>
                </div>
                
                <div class="menu-item">
                    <div class="item-info">
                        <h3>Hamburguesa Clásica</h3>
                        <p>Carne de res, queso, lechuga, tomate y salsa especial.</p>
                        <div class="item-controls">
                            <button class="quantity-btn minus" data-item="Hamburguesa Clásica" data-price="10.99">-</button>
                            <span class="quantity-display" id="qty-Hamburguesa Clásica">0</span>
                            <button class="quantity-btn plus" data-item="Hamburguesa Clásica" data-price="10.99">+</button>
                        </div>
                    </div>
                    <div class="item-price">$10.99</div>
                </div>
                
                <div class="menu-item">
                    <div class="item-info">
                        <h3>Filete de Salmón</h3>
                        <p>Salmón a la parrilla con vegetales asados y puré de papas.</p>
                        <div class="item-controls">
                            <button class="quantity-btn minus" data-item="Filete de Salmón" data-price="16.50">-</button>
                            <span class="quantity-display" id="qty-Filete de Salmón">0</span>
                            <button class="quantity-btn plus" data-item="Filete de Salmón" data-price="16.50">+</button>
                        </div>
                    </div>
                    <div class="item-price">$16.50</div>
                </div>
            </div>
            
            <!-- Categoría Bebidas -->
            <div class="category">
                <h2><i class="fas fa-glass-cheers"></i> Bebidas</h2>
                
                <div class="menu-item">
                    <div class="item-info">
                        <h3>Refresco de Cola</h3>
                        <p>Refresco de cola en lata (330ml).</p>
                        <div class="item-controls">
                            <button class="quantity-btn minus" data-item="Refresco de Cola" data-price="2.50">-</button>
                            <span class="quantity-display" id="qty-Refresco de Cola">0</span>
                            <button class="quantity-btn plus" data-item="Refresco de Cola" data-price="2.50">+</button>
                        </div>
                    </div>
                    <div class="item-price">$2.50</div>
                </div>
                
                <div class="menu-item">
                    <div class="item-info">
                        <h3>Jugo Natural</h3>
                        <p>Jugo de naranja recién exprimido (500ml).</p>
                        <div class="item-controls">
                            <button class="quantity-btn minus" data-item="Jugo Natural" data-price="4.00">-</button>
                            <span class="quantity-display" id="qty-Jugo Natural">0</span>
                            <button class="quantity-btn plus" data-item="Jugo Natural" data-price="4.00">+</button>
                        </div>
                    </div>
                    <div class="item-price">$4.00</div>
                </div>
                
                <div class="menu-item">
                    <div class="item-info">
                        <h3>Agua Mineral</h3>
                        <p>Botella de agua mineral sin gas (500ml).</p>
                        <div class="item-controls">
                            <button class="quantity-btn minus" data-item="Agua Mineral" data-price="1.99">-</button>
                            <span class="quantity-display" id="qty-Agua Mineral">0</span>
                            <button class="quantity-btn plus" data-item="Agua Mineral" data-price="1.99">+</button>
                        </div>
                    </div>
                    <div class="item-price">$1.99</div>
                </div>
            </div>
        </div>

        <div class="cart-container">
            <div class="cart-header">
                <h2><i class="fas fa-shopping-cart"></i> Tu Pedido</h2>
                <button id="clearCart">Vaciar Carrito</button>
            </div>
            
            <div id="cartItems">
                <!-- Los productos seleccionados aparecerán aquí -->
                <p id="emptyCartMessage" style="text-align: center; color: var(--gray-color);">Tu carrito está vacío. Selecciona productos del menú.</p>
            </div>
            
            <div class="cart-total">
                <span>Total:</span>
                <span id="cartTotal">$0.00</span>
            </div>
            
            <div class="cart-actions">
                <button id="sendOrder">
                    <i class="fab fa-whatsapp"></i> Enviar Pedido por WhatsApp
                </button>
            </div>
        </div>

        <div class="instructions">
            <h3><i class="fas fa-info-circle"></i> Cómo hacer tu pedido</h3>
            <ol>
                <li>Selecciona los productos que deseas ordenar usando los botones "+" y "-".</li>
                <li>Revisa tu pedido en la sección "Tu Pedido".</li>
                <li>Haz clic en "Enviar Pedido por WhatsApp" para generar un mensaje con tu pedido.</li>
                <li>Se abrirá WhatsApp con el mensaje predefinido. Solo debes seleccionar el contacto del restaurante y enviar.</li>
                <li>También puedes escanear el código QR para compartir el menú con tus amigos.</li>
            </ol>
        </div>

        <footer>
            <p>Restaurante "Sabor a Casa" &copy; 2023 | Menú Digital con Pedidos por WhatsApp</p>
        </footer>
    </div>

    <script>
        // Variables globales
        let cart = {};
        const phoneNumber = "1234567890"; // Número de WhatsApp del restaurante
        
        // Inicializar carrito desde localStorage si existe
        document.addEventListener('DOMContentLoaded', function() {
            const savedCart = localStorage.getItem('restaurantCart');
            if (savedCart) {
                cart = JSON.parse(savedCart);
                updateCartDisplay();
            }
            
            // Generar código QR
            generateQRCode();
            
            // Agregar event listeners a los botones de cantidad
            document.querySelectorAll('.quantity-btn.plus').forEach(button => {
                button.addEventListener('click', function() {
                    const item = this.getAttribute('data-item');
                    const price = parseFloat(this.getAttribute('data-price'));
                    addToCart(item, price);
                });
            });
            
            document.querySelectorAll('.quantity-btn.minus').forEach(button => {
                button.addEventListener('click', function() {
                    const item = this.getAttribute('data-item');
                    removeFromCart(item);
                });
            });
            
            // Event listeners para botones del carrito
            document.getElementById('clearCart').addEventListener('click', clearCart);
            document.getElementById('sendOrder').addEventListener('click', sendOrder);
        });
        
        // Función para agregar producto al carrito
        function addToCart(item, price) {
            if (cart[item]) {
                cart[item].quantity += 1;
            } else {
                cart[item] = { price: price, quantity: 1 };
            }
            
            updateCartDisplay();
            saveCartToStorage();
        }
        
        // Función para eliminar producto del carrito
        function removeFromCart(item) {
            if (cart[item]) {
                cart[item].quantity -= 1;
                
                if (cart[item].quantity <= 0) {
                    delete cart[item];
                }
                
                updateCartDisplay();
                saveCartToStorage();
            }
        }
        
        // Función para actualizar la visualización del carrito
        function updateCartDisplay() {
            const cartItemsContainer = document.getElementById('cartItems');
            const emptyCartMessage = document.getElementById('emptyCartMessage');
            const cartTotalElement = document.getElementById('cartTotal');
            
            // Actualizar contadores en los productos del menú
            for (const item in cart) {
                const quantityElement = document.getElementById(`qty-${item}`);
                if (quantityElement) {
                    quantityElement.textContent = cart[item].quantity;
                }
            }
            
            // Si el carrito está vacío, mostrar mensaje
            if (Object.keys(cart).length === 0) {
                cartItemsContainer.innerHTML = '<p id="emptyCartMessage" style="text-align: center; color: var(--gray-color);">Tu carrito está vacío. Selecciona productos del menú.</p>';
                cartTotalElement.textContent = '$0.00';
                return;
            }
            
            // Si hay productos, generar la lista del carrito
            let cartHTML = '';
            let total = 0;
            
            for (const item in cart) {
                const itemTotal = cart[item].price * cart[item].quantity;
                total += itemTotal;
                
                cartHTML += `
                    <div class="cart-item">
                        <div class="cart-item-name">${item}</div>
                        <div class="cart-item-quantity">${cart[item].quantity}</div>
                        <div class="cart-item-price">$${itemTotal.toFixed(2)}</div>
                    </div>
                `;
            }
            
            cartItemsContainer.innerHTML = cartHTML;
            cartTotalElement.textContent = `$${total.toFixed(2)}`;
        }
        
        // Función para vaciar el carrito
        function clearCart() {
            cart = {};
            updateCartDisplay();
            saveCartToStorage();
            
            // Reiniciar contadores de productos
            document.querySelectorAll('.quantity-display').forEach(element => {
                element.textContent = '0';
            });
        }
        
        // Función para guardar carrito en localStorage
        function saveCartToStorage() {
            localStorage.setItem('restaurantCart', JSON.stringify(cart));
        }
        
        // Función para generar mensaje de WhatsApp
        function generateWhatsAppMessage() {
            let message = `¡Hola! Me gustaría hacer un pedido:\n\n`;
            
            for (const item in cart) {
                message += `- ${item} x${cart[item].quantity}: $${(cart[item].price * cart[item].quantity).toFixed(2)}\n`;
            }
            
            const total = Object.keys(cart).reduce((sum, item) => sum + (cart[item].price * cart[item].quantity), 0);
            message += `\nTotal: $${total.toFixed(2)}\n\nGracias.`;
            
            return encodeURIComponent(message);
        }
        
        // Función para enviar pedido por WhatsApp
        function sendOrder() {
            if (Object.keys(cart).length === 0) {
                alert('Tu carrito está vacío. Agrega productos antes de enviar el pedido.');
                return;
            }
            
            const message = generateWhatsAppMessage();
            const whatsappURL = `https://wa.me/${phoneNumber}?text=${message}`;
            
            // Abrir WhatsApp en una nueva pestaña
            window.open(whatsappURL, '_blank');
            
            // Opcional: Limpiar el carrito después de enviar
            // clearCart();
        }
        
        // Función para generar código QR
        function generateQRCode() {
            const currentURL = window.location.href;
            const qrCodeElement = document.getElementById('qrCode');
            
            // Limpiar el elemento antes de generar nuevo QR
            qrCodeElement.innerHTML = '';
            
            // Generar código QR
            QRCode.toCanvas(qrCodeElement, currentURL, {
                width: 160,
                height: 160,
                margin: 1,
                color: {
                    dark: '#075E54',
                    light: '#FFFFFF'
                }
            }, function(error) {
                if (error) console.error(error);
            });
        }
    </script>
</body>
</html>
