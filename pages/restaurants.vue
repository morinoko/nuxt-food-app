<template>
  <section class="container restaurant">
    <div class="restaurantheading">
      <h1>Restaurants</h1>

      <AppSelect @change="selectedRestaurant = $event" />
    </div>
    <AppRestaurantInfo :datasource="filteredRestaurants"/>
  </section>
</template>

<script>
import AppRestaurantInfo from "@/components/AppRestaurantInfo";
import AppSelect from "@/components/AppSelect";
import { mapState } from 'vuex';

export default {
  components: {
    AppRestaurantInfo,
    AppSelect
  },
  data() {
    return {
      selectedRestaurant: ''
    }
  },
  computed: {
    ...mapState([
      'fooddata'
    ]),
    filteredRestaurants() {
      if (this.selectedRestaurant) {
        return this.fooddata.filter(el => {
          let name = el.name.toLowerCase();
          return name.includes(this.selectedRestaurant);
        })
      }
      return this.fooddata;
    }
  }
}
</script>

<style scoped>
</style>
