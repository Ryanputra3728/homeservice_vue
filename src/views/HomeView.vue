<template>
  <div class="container">
    <h1 class="mt-5 mb-4">Product List</h1>

    <!-- Search Bar -->
<div class="mb-4">
  <label for="search" class="form-label">Search Product:</label>
  <input v-model="searchQuery" type="text" id="search" class="form-control custom-search" @input="searchProducts" />
</div>


    <div class="row">
      <div v-for="product in filteredProducts" :key="product.id" class="col-md-4">
        <div class="product-card mb-4" @mouseover="hoverCard(true)" @mouseout="hoverCard(false)">
          <img :src="product.thumbnail" :alt="product.title" class="img-fluid mb-3" />
          <h3>{{ product.title }}</h3>
          <p>{{ product.description }}</p>
          <p class="price">Price: <span class="currency">$</span>{{ product.price }}</p>
          <p class="stock">Stock: {{ product.stock }}</p>
          <button @click="addToCart(product)" class="btn btn-primary">Add to Cart</button>
        </div>
      </div>
    </div>

    <!-- Shopping Cart -->
    <div class="cart-container">
      <div class="shopping-cart">
        <h2>Shopping Cart</h2>
        <ul>
          <li v-for="item in cart" :key="item.id">
            {{ item.title }} - ${{ item.price }} - Quantity: {{ item.quantity }}
            <span @click="removeOneFromCart(item)" class="delete-link">Delete</span>
          </li>
        </ul>
        <p><strong>Total Price: ${{ totalPrice.toFixed(2) }}</strong></p>
           <!-- Confirm Shopping Cart button -->
        <button v-if="cart.length > 0" @click="confirmShoppingCart" class="btn btn-success">Confirm Shopping Cart</button>
      </div>  
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      products: [],
      filteredProducts: [],
      isHovered: false,
      cart: [],
      searchQuery: "",
    };
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((total, item) => total + item.price * item.quantity, 0);
    },
  },
  mounted() {
    this.fetchProducts();
  },
  methods: {
    async fetchProducts() {
      try {
        const response = await axios.get("https://dummyjson.com/products");
        this.products = response.data.products;
        this.filteredProducts = this.products; // Initialize filteredProducts with all products
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },
    hoverCard(value) {
      this.isHovered = value;
    },
    addToCart(product) {
      const cartItem = this.cart.find((item) => item.id === product.id);

      if (cartItem) {
        cartItem.quantity++;
      } else {
        if (product.stock > 0) {
          this.cart.push({
            id: product.id,
            title: product.title,
            price: product.price,
            quantity: 1,
          });
          product.stock--;
        } else {
          alert("Product is out of stock");
        }
      }
    },
    removeOneFromCart(item) {
      const index = this.cart.indexOf(item);
      if (index !== -1) {
        const product = this.products.find((p) => p.id === item.id);
        if (product) {
          product.stock++;
        }

        if (item.quantity > 1) {
          item.quantity--;
        } else {
          this.cart.splice(index, 1);
        }
      }
    },
    searchProducts() {
      // Filter products based on the search query
      this.filteredProducts = this.products.filter((product) =>
        product.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
    confirmShoppingCart() {
      // Add your logic to handle the confirmation of the shopping cart
      alert("Shopping cart confirmed!");
    },
  },
};
</script>

<style scoped>

.custom-search {
  width: 300px; /* Set the desired width for the search bar */
  border: 1px solid #ced4da; /* Add border style */
  border-radius: 5px; /* Add border radius for rounded corners */
  padding: 8px; /* Add padding for better appearance */
}

.product-card {
  text-align: center;
  border: 1px solid #ccc;
  padding: 15px;
  transition: border-color 0.3s ease-in-out;
}

.product-card:hover {
  border-color: #007bff; /* Change this to the desired hover color */
}

.product-card img {
  max-width: 100%;
  height: auto;
}

.price {
  font-size: 1.2em;
}

.currency {
  font-weight: bold;
  margin-right: 3px;
}

.stock {
  font-size: 1em;
  color: #28a745; /* Green color for stock information */
}

.cart-container {
  position: fixed;
  bottom: 20px;
  right: 20px;
  z-index: 1000;
}

.shopping-cart {
  background-color: #fff;
  border: 1px solid #ccc;
  padding: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.delete-link {
  color: red;
  cursor: pointer;
  margin-left: 10px;
}
</style>
