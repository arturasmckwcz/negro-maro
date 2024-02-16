<template>
  <main class="wrapper">
    <h2>Recommended</h2>

    <div class="recommended">
      <CardComponent
        class="card"
        v-for="product in cards"
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
  props: ["inventory", "recommended", "addToCart"],
  // data() {
  //   return {
  //     cards: this.inventory.filter(({ id }) => this.recommended.includes(id)),
  //   };
  // },
  computed: {
    cards() {
      const cards = this.inventory.filter(({ id }) =>
        this.recommended.includes(id)
      );
      return cards;
    },
  },
};
</script>
