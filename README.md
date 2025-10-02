from flask import Flask, render_template

app = Flask(__name__)

# Liste des produits (exemple)
products = [
    {"id": 1, "name": "Laptop", "price": 1200, "description": "Ordinateur portable performant"},
    {"id": 2, "name": "Smartphone", "price": 800, "description": "Smartphone avec écran AMOLED"},
    {"id": 3, "name": "Headphones", "price": 150, "description": "Casque audio de haute qualité"},
]

@app.route('/')
def index():
    return render_template('index.html', products=products)

@app.route('/product/<int:product_id>')
def product_detail(product_id):
    # Trouver le produit correspondant
    product = next((p for p in products if p["id"] == product_id), None)
    if product:
        return render_template('product.html', product=product)
    else:
        return "Produit non trouvé", 404

if __name__ == '__main__':
    app.run(debug=True)
