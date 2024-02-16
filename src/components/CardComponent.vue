<template>
  <main class="wrapper">
    <div class="card">
      <div class="card-title">{{ product.name }}</div>
      <div class="card-body">
        <i :class="iconClassName"></i>
        <form>
          <div class="row">
            <div class="cell">
              <label>Type:</label>
            </div>
            <div class="cell">
              <em>{{ product.type }}</em>
            </div>
          </div>
          <div class="row">
            <div class="cell">
              <label>Price:</label>
            </div>
            <div class="cell">${{ product.price.USD.toFixed(2) }}</div>
          </div>
          <div class="row">
            <div class="cell">
              <label>Quantity:</label>
            </div>
            <div class="cell">
              <input type="number" v-model.number="quantity" />
            </div>
          </div>
        </form>
      </div>
      <div class="card-footer">
        <button class="btn btn-light" @click="handleAddToCart">
          Add to cart
        </button>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "CardComponent",
  props: ["product", "addToCart"],
  data() {
    return {
      quantity: "",
      iconClassName: `icofont-10x icofont-${this.product.icon}`,
    };
  },
  methods: {
    handleAddToCart() {
      this.addToCart(this.product, this.quantity);
      this.quantity = "";
    },
  },
};
</script>
