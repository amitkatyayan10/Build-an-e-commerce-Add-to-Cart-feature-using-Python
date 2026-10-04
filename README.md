# Build-an-e-commerce-Add-to-Cart-feature-using-Python
Build an e-commerce Add to Cart feature using Python

Demo 1: Build an e-commerce Add to Cart feature using Python
Step 1: Define the products
products = {
    101: {"name": "Headphones", "price": 1999},
    102: {"name": "Smart Watch", "price": 2999},
    103: {"name": "Laptop Bag", "price": 999}
}
Explanation:

products is a dictionary.
101, 102 and 103 are product IDs.
Each ID has a product name and price.
In a real e-commerce application, this data would normally be stored in a database rather than being hardcoded in Python

Step 2: Create an empty cart
cart = []

The square brackets [] create an empty list.

Initially, the customer has not added anything.

Step 3: Add a product to the cart
def add_to_cart(product_id, quantity):
    if product_id in products:
        cart.append({
            "product_id": product_id,
            "quantity": quantity
        })
        print("Product added successfully")
    else:
        print("Product not found")

add_to_cart(101, 2)

Expected output:

Product added successfully

What is happening?

def creates a function.

add_to_cart is the function name.

product_id and quantity are inputs.

if checks whether the product exists.

append() adds the product to the cart.

Here we have created the basic business logic for adding a product.

Step 4: Calculate the cart total
def calculate_total():
    total = 0

    for item in cart:
        product_id = item["product_id"]
        quantity = item["quantity"]

        price = products[product_id]["price"]
        total = total + (price * quantity)

    return total

print(calculate_total())

Output:

3998

The calculation is:

2 headphones × ₹1,999 = ₹3,998.

The important concept is that a function can combine product prices and quantities to calculate the total automatically.

Step 5: Turn the code into an API

Real applications usually need an API endpoint so the frontend can communicate with the backend. For beginners, Flask is a simple Python framework to understand this process.

Install Flask:

pip install flask

Create a file called app.py:

from flask import Flask, jsonify, request

app = Flask(__name__)

products = {
    101: {"name": "Headphones", "price": 1999},
    102: {"name": "Smart Watch", "price": 2999}
}

cart = []

@app.route("/cart/add", methods=["POST"])
def add_to_cart():
    data = request.get_json()

    product_id = data.get("product_id")
    quantity = data.get("quantity", 1)

    if product_id not in products:
        return jsonify({"error": "Product not found"}), 404

    if not isinstance(quantity, int) or quantity < 1:
        return jsonify({"error": "Invalid quantity"}), 400

    cart.append({
        "product_id": product_id,
        "quantity": quantity
    })

    return jsonify({
        "message": "Added to cart",
        "cart": cart
    })

if __name__ == "__main__":
    app.run(debug=True)

This is a simplified demonstration API. It does not yet support user accounts, persistent storage, duplicate item consolidation, inventory checks or production security.
