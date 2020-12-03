<template>
  <main class="container">
    <AppHeader />
    <AppRestaurantInfo :datasource="fooddata" />
  </main>
</template>

<script>
import AppHeader from "@/components/AppHeader";
import AppRestaurantInfo from "@/components/AppRestaurantInfo";
import { mapState } from "vuex";

export default {
  components: {
    AppHeader,
    AppRestaurantInfo,
  },
  computed: {
    ...mapState([
      'fooddata'
    ])
  },
}
</script>

<style>
</style>
