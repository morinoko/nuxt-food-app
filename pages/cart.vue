<template>
  <main class="container cart">
    <h2>Your Cart</h2>
    <AppEmptyCart />
    <table v-if="cart.length">
      <thead>
        <tr>
          <th>Item</th>
          <th>Add Ons</th>
          <th>Amount</th>
          <th>Total Price</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in cart" :key="item.id">
          <td>
            {{ item.item }}
            <span v-if="item.option">- {{ item.option }}</span>
          </td>
          <td>
            <span
              v-for="addOn in item.addOns"
              :key="addOn"
              class="comma"
            >
              {{ addOn }}
            </span>
          </td>
          <td>{{ item.quantity }}</td>
          <td>{{ item.total }}</td>
        </tr>
        <tr>
          <td colspan="3"></td>
          <td class="total">Total: ${{  cartTotal.toFixed(2) }}</td>
        </tr>
      </tbody>
    </table>
  </main>
</template>

<script>
import { mapState, mapGetters } from "vuex";
import AppEmptyCart from "@/components/AppEmptyCart";

export default {
  components: {
    AppEmptyCart
  },
  computed: {
    ...mapState(["cart"]),
    ...mapGetters(["cartTotal"])
  }
}
</script>

<style scoped>

</style>
