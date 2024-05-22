<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Customer Order Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }
        .container {
            max-width: 600px;
            margin: 20px auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        input[type="text"], input[type="email"], input[type="tel"], select {
            width: calc(100% - 12px);
            padding: 8px;
            margin: 8px 0;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
        }
        input[type="submit"] {
            background-color: #4caf50;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        input[type="submit"]:hover {
            background-color: #45a049;
        }
        label {
            font-weight: bold;
        }

        /* Modal styles */
        .modal {
            display: none;
            position: fixed;
            z-index: 1;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0,0,0,0.4);
        }

        .modal-content {
            background-color: #fefefe;
            margin: 15% auto;
            padding: 20px;
            border: 1px solid #888;
            width: 80%;
            border-radius: 8px;
        }

        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
        }

        .close:hover,
        .close:focus {
            color: black;
            text-decoration: none;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Customer Order Form</h2>
        <form id="orderForm" action="#" method="post">
            <!-- Customer Information -->
            <h3>Customer Information</h3>
            <label for="fullname">Full Name:</label>
            <input type="text" id="fullname" name="fullname" required>
            <label for="email">Email Address:</label>
            <input type="email" id="email" name="email" required>
            <label for="phone">Phone Number:</label>
            <input type="tel" id="phone" name="phone" required>
            
            <!-- Order Details -->
            <h3>Order Details</h3>
            <label for="date">Date of Order:</label>
            <input type="date" id="date" name="date" required><br><br>
            <label>Delivery/Pickup Preference:</label><br>
            <input type="radio" id="delivery" name="delivery_preference" value="Delivery" required>
            <label for="delivery">Delivery</label><br>
            <input type="radio" id="pickup" name="delivery_preference" value="Pickup" required>
            <label for="pickup">Pickup</label><br>
            <label for="address">Delivery Address:</label>
            <input type="text" id="address" name="address">
            <label for="pickup_location">Pickup Location:</label>
            <input type="text" id="pickup_location" name="pickup_location">
            
            <!-- Product Selection -->
            <h3>Product Selection</h3>
            <label>Cupcakes:</label><br>
            <input type="checkbox" id="chocolate_cupcake" name="cupcakes[]" value="Chocolate">
            <label for="chocolate_cupcake">Chocolate</label><br>
            <input type="checkbox" id="vanilla_cupcake" name="cupcakes[]" value="Vanilla">
            <label for="vanilla_cupcake">Vanilla</label><br>
            <input type="checkbox" id="redvelvet_cupcake" name="cupcakes[]" value="Red Velvet">
            <label for="redvelvet_cupcake">Red Velvet</label><br>
            
            <label>Cakes:</label><br>
            <select id="cakes" name="cakes">
                <option value="--" selected>--</option>
                <option value="Small">Small</option>
                <option value="Medium">Medium</option>
                <option value="Large">Large</option>
            </select><br>
            
            <label>Cookies:</label><br>
            <input type="checkbox" id="chocolate_chip" name="cookies[]" value="Chocolate Chips">
            <label for="chocolate_chip">Chocolate Chips</label><br>
            <input type="checkbox" id="oatmeal" name="cookies[]" value="Oatmeal">
            <label for="oatmeal">Oatmeal</label><br>
            <input type="checkbox" id="sugar" name="cookies[]" value="Sugar">
            <label for="sugar">Sugar</label><br>
            
            <label>Pastries:</label><br>
            <input type="checkbox" id="croissants" name="pastries[]" value="Croissants">
            <label for="croissants">Croissants</label><br>
            <input type="checkbox" id="danishes" name="pastries[]" value="Danishes">
            <label for="danishes">Danishes</label><br>
            <input type="checkbox" id="muffins" name="pastries[]" value="Muffins">
            <label for="muffins">Muffins</label><br>
            
            <!-- Payment Information -->
            <h3>Payment Information</h3>
            <label>Payment Method:</label><br>
            <input type="radio" id="creditcard" name="payment_method" value="Credit Card" required>
            <label for="creditcard">Credit Card</label><br>
            <input type="radio" id="paypal" name="payment_method" value="PayPal">
            <label for="paypal">PayPal</label><br>
            <input type="radio" id="cashondelivery" name="payment_method" value="Cash on Delivery">
            <label for="cashondelivery">Cash on Delivery</label><br>
           
            <!-- Credit Card Information -->
            <div id="creditCardInfo" style="display: none;">
                <label for="cardnumber">Credit Card Number:</label>
                <input type="text" id="cardnumber" name="cardnumber">
                <label for="expiry">Expiry Date:</label>
                <input type="month" id="expiry" name="expiry">
                <label for="cvv">CVV:</label>
                <input type="text" id="cvv" name="cvv">
            </div>

            <!-- PayPal Information -->
            <div id="paypalInfo" style="display: none;">
                <label for="paypal_email">PayPal Email:</label>
                <input type="email" id="paypal_email" name="paypal_email">
            </div>

            <br>
            <!-- Submit Button -->
            <input type="submit" value="Submit Order">
        </form>
    </div>

    <!-- Modal -->
    <div id="myModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <p>Thank you for your order!</p>
        </div>
    </div>

    <script>
        // JavaScript code for showing/hiding credit card fields based on payment method selection
        var paymentMethodRadios = document.querySelectorAll('input[name="payment_method"]');
        var creditCardInfo = document.getElementById('creditCardInfo');
        var paypalInfo = document.getElementById('paypalInfo');

        paymentMethodRadios.forEach(function(radio) {
            radio.addEventListener('change', function() {
                if (this.value === 'Credit Card') {
                    creditCardInfo.style.display = 'block';
                    paypalInfo.style.display = 'none';
                } else if (this.value === 'PayPal') {
                    creditCardInfo.style.display = 'none';
                    paypalInfo.style.display = 'block';
                } else {
                    creditCardInfo.style.display = 'none';
                    paypalInfo.style.display = 'none';
                }
            });
        });

// JavaScript code for showing/hiding modal after form submission
var modal = document.getElementById("myModal");
        var span = document.getElementsByClassName("close")[0];

        document.getElementById("orderForm").addEventListener("submit", function(event) {
            // Prevent the default form submission behavior
            event.preventDefault();

            // Check if the form is valid
            if (this.checkValidity()) {
                // Display the modal if the form is valid
                modal.style.display = "block";
            } else {
                // If the form is not valid, focus on the first invalid field
                var invalidField = this.querySelector(':invalid');
                invalidField.focus();
            }
        });

        span.onclick = function() {
            modal.style.display = "none";
        };

        window.onclick = function(event) {
            if (event.target == modal) {
                modal.style.display = "none";
            }
        };
    </script>
</body>
</html>
