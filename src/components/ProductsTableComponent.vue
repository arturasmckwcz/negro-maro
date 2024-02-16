<template>
  <table :class="tableClassName">
    <thead>
      <tr>
        <th><span class="sr-only">Product Image</span></th>
        <th>Product</th>
        <th>Price</th>
        <th>Qty</th>
        <th>Total</th>
        <th><span class="sr-only">Actions</span></th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in items" :key="item.id">
        <td><i :class="iconClassName(item)"></i></td>
        <td>{{ item.name }}</td>
        <td>${{ item.price }}</td>
        <td>{{ item.quantity }}</td>
        <td>${{ (item.quantity * item.price).toFixed(2) }}</td>
        <td class="center">
          <button :class="buttonClassName" @click="handleButtonClick(item.id)">
            {{ buttonText }}
          </button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "ProductsTableComponent",
  props: ["items", "handleButtonClick", "cart"],
  computed: {
    buttonText() {
      return this.cart ? "×" : "Add";
    },
    buttonClassName() {
      return this.cart ? "btn btn-light cart-remove" : "btn btn-dark";
    },
    tableClassName() {
      return this.cart ? "cart-table" : "product-table";
    },
  },
  methods: {
    iconClassName(item) {
      return `icofont-${item.icon} icofont-${this.cart ? "3" : "4"}x`;
    },
  },
};
</script>

<style scoped>
th {
  text-align: start;
}
</style>
