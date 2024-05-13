<!-- index.php -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Order Management System</title>
    <style>

        body {
            background-color: #8B322C; 
        }

        .container {
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
            background-color: #DD5746;
        }

        input[type="text"], input[type="number"], select, button {
            display: block;
            margin-bottom: 10px;
        }

        button {
            padding: 10px 20px;
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        button:hover {
            background-color: #0056b3;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        th, td {
            padding: 8px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }

        th {
            background-color: #f2f2f2;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Order Management System</h1>
        <?php
        // Define menu items with prices in pesos
        $menu = [
            'Burger' => 75,
            'Coke Float' => 65,
            'Fries' => 50,
            'Spaghetti' => 89
        ];

        // Initialize orders array
        $orders = [];

        // Process order form submission
        if ($_SERVER["REQUEST_METHOD"] == "POST") {
            $item = $_POST['item'];
            $quantity = $_POST['quantity'];
            $price = $menu[$item] * $quantity;
            $cash = $_POST['cash'];
            
            // Add order details to orders array
            $orders[] = ['item' => $item, 'quantity' => $quantity, 'price' => $price, 'cash' => $cash];
        }
        ?>
        <form action="" method="post">
            <label for="item">Select Item:</label>
            <select id="item" name="item" required>
                <?php
                // Display menu items
                foreach ($menu as $menuItem => $price) {
                    echo "<option value='$menuItem'>$menuItem (₱$price)</option>";
                }
                ?>
            </select>
            <label for="quantity">Quantity:</label>
            <input type="number" id="quantity" name="quantity" min="1" required>
            <label for="cash">Cash (₱):</label>
            <input type="number" id="cash" name="cash" min="0" required>
            <button type="submit">Submit Order</button>
        </form>
        <hr>
        <h2>Receipt</h2>
        <table>
            <thead>
                <tr>
                    <th>Item</th>
                    <th>Quantity</th>
                    <th>Total Price (₱)</th>
                    <th>Cash (₱)</th>
                    <th>Change (₱)</th>
                </tr>
            </thead>
            <tbody>
                <?php
                // Display receipt details
                foreach ($orders as $order) {
                    $change = $order['cash'] - $order['price'];
                    echo "<tr>";
                    echo "<td>{$order['item']}</td>";
                    echo "<td>{$order['quantity']}</td>";
                    echo "<td>{$order['price']}</td>";
                    echo "<td>{$order['cash']}</td>";
                    echo "<td>$change</td>";
                    echo "</tr>";
                }
                ?>
            </tbody>
        </table>
    </div>
</body>
</html>
