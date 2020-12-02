<template>
  <section class="container restaurant">
    <h1 class="restaurantheading">Restaurants</h1>
    <AppRestaurantInfo />
  </section>
</template>

<script>
import AppRestaurantInfo from "@/components/AppRestaurantInfo";

export default {
  components: {
    AppRestaurantInfo,
  }
}
</script>

<style scoped>
</style>
