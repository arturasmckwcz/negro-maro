<template>
  <SplashComponent />
  <main v-if="true" class="wrapper">
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
import SplashComponent from "@/components/SplashComponent.vue";
import CardComponent from "@/components/CardComponent.vue";

export default {
  name: "HomeView",
  components: { SplashComponent, CardComponent },
  props: ["inventory", "recommended", "addToCart"],
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
