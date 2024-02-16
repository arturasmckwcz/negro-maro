<template>
  <aside class="cart-container">
    <div class="cart">
      <h1 class="cart-title spread">
        <span>
          Cart
          <i class="icofont-cart-alt icofont-1x"></i>
        </span>
        <button class="cart-close" @click="toggle">&times;</button>
      </h1>

      <div class="cart-body">
        <ProductsTableComponent
          :inventory="inventory"
          :items="cartContent"
          :handleButtonClick="deleteFromCart"
          :cart="true"
        />

        <p class="center">
          <em v-if="cartContent.length === 0">No items in cart</em>
        </p>
        <div class="spread">
          <span><strong>Total:</strong> ${{ computedTotal.toFixed(2) }}</span>
          <button class="btn btn-light" @click="checkoutCart(cartContent)">
            Checkout
          </button>
        </div>
      </div>
    </div>
  </aside>
</template>

<script>
import ProductsTableComponent from "@/components/ProductsTableComponent.vue";

export default {
  name: "SidebarComponent",
  components: { ProductsTableComponent },
  props: ["toggle", "cart", "inventory", "deleteFromCart", "checkoutCart"],
  methods: {
    iconClassName(item) {
      return `icofont-${item.icon} icofont-3x`;
    },
  },
  computed: {
    cartContent() {
      return Object.keys(this.cart).map((item) => {
        const product = this.inventory.find(({ id }) => id == item);
        return {
          quantity: this.cart[item],
          id: product.id,
          name: product.name,
          icon: product.icon,
          price: product.price.USD,
        };
      });
    },
    computedTotal() {
      return this.cartContent.reduce((result, item) => {
        return result + item.quantity * item.price;
      }, 0);
    },
  },
};
</script>
