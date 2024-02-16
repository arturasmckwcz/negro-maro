<template>
  <SplashComponent />
  <RecommendedComponent
    :inventory="inventory"
    :recommended="recommended"
    :addToCart="addToCart"
  />
</template>

<script>
import SplashComponent from "@/components/SplashComponent.vue";
import RecommendedComponent from "@/components/RecommendedComponent.vue";

export default {
  name: "HomeView",
  components: { SplashComponent, RecommendedComponent },
  props: ["inventory", "recommended", "addToCart"],
};
</script>
