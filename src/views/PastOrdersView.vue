<template>
  <main class="wrapper">
    <h1>Past Orders</h1>

    <ProductsTableComponent
      :inventory="inventory"
      :items="pastOrders"
      :handleButtonClick="handleAddToCart"
    />

    <div v-if="pastOrders.length > 0" class="spread mt-1">
      <span></span>
      <button class="btn btn-dark" @click="clearPostOrders">
        &times; Clear
      </button>
    </div>
  </main>
</template>

<script>
import ProductsTableComponent from "@/components/ProductsTableComponent.vue";

export default {
  name: "PastOrdersView",
  props: ["inventory", "pastOrders", "addToCart", "clearPostOrders"],
  components: { ProductsTableComponent },
  methods: {
    handleAddToCart(productId) {
      const product = this.inventory.find(({ id }) => id === productId);
      const quantity = this.pastOrders.find(
        ({ id }) => id === productId
      ).quantity;
      this.addToCart(product, quantity);
    },
  },
};
</script>

<style scoped>
.mt-1 {
  margin-top: 1em;
}
</style>
