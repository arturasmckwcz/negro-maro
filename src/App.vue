<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link>
      <router-link to="/products" class="top-bar-link">
        <span>Products</span>
      </router-link>
      <router-link to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>
    <a @click="toggleSidebar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span>Cart({{ numSelected }})</span>
    </a>
  </header>

  <router-view
    :inventory="inventory"
    :recommended="recommended"
    :cart="cart"
    :addToCart="addToCart"
    :pastOrders="pastOrders"
    :clearPostOrders="clearPostOrders"
  />

  <SidebarComponent
    v-if="showSidebar"
    :toggle="toggleSidebar"
    :cart="cart"
    :inventory="inventory"
    :deleteFromCart="deleteFromCart"
    :checkoutCart="checkoutCart"
  />
</template>
<script>
import SidebarComponent from "./components/SidebarComponent.vue";
import productData from "@/assets/data/food.json";

export default {
  components: { SidebarComponent },
  data() {
    return {
      showSidebar: false,
      inventory: productData.inventory,
      recommended: productData.recommended,
      cart: {},
      pastOrders: [],
    };
  },
  computed: {
    numSelected() {
      return Object.keys(this.cart).length;
    },
  },
  methods: {
    addToCart(product, quantity) {
      if (!this.cart[product.id]) this.cart[product.id] = 0;
      this.cart[product.id] += quantity;
    },
    deleteFromCart(id) {
      delete this.cart[id];
    },
    checkoutCart(cartContent) {
      cartContent.forEach((item) => this.pastOrders.push(item));
      this.cart = {};
      this.showSidebar = false;
    },
    clearPostOrders() {
      this.pastOrders = [];
    },
    toggleSidebar() {
      this.showSidebar = !this.showSidebar;
    },
  },
};
</script>
