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
// @ is an alias to /src

export default {
  name: "HomeView",
  components: { SplashComponent, RecommendedComponent },
  props: ["inventory", "recommended", "addToCart"],
};
</script>
