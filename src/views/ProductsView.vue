<template>
  <main class="wrapper">
    <h1>Products</h1>

    <div class="card-container">
      <CardComponent
        class="card"
        v-for="product in inventory"
        :product="product"
        :key="product.id"
        :addToCart="addToCart"
      ></CardComponent>
    </div>
  </main>
</template>

<script>
import CardComponent from "@/components/CardComponent.vue";

export default {
  components: { CardComponent },
  name: "RecommendedComponent",
  props: ["inventory", "addToCart"],
};
</script>
