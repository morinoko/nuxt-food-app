<template>
  <main class="container">
    <section
      class="image"
      :style="`background: url(/${currentItem.img}) no-repeat center center`"
    ></section>

    <section class="details">
      <h1>{{ currentItem.item }}</h1>
      <h3>Price: ${{ currentItem.price.toFixed(2) }}</h3>
      <div class="quantity">
        <input type="number" min="1" value="1" v-model="quantity">
        <button class="primary" @click="addToCart">
          Add to Cart - ${{ total }}
        </button>
      </div>

      <fieldset v-if="currentItem.options">
        <legend>
          <h3>Options</h3>
        </legend>
        <div v-for="option in currentItem.options" :key="option">
          <input
            type="radio"
            name="option"
            :id="option"
            :value="option"
            v-model="selectedOption"
          />
          <label :for="option">{{ option }}</label>
        </div>
      </fieldset>

      <fieldset v-if="currentItem.addOns">
        <legend>
          <h3>Add Ons</h3>
        </legend>
        <div v-for="addOn in currentItem.addOns" :key="addOn">
          <input
            type="checkbox"
            name="addon"
            :id="addOn"
            :value="addOn"
            v-model="selectedAddOns"
          />
          <label :for="addOn">{{ addOn }}</label>
        </div>
      </fieldset>

      <AppToast v-if="cartSubmitted">
        Order submitted <br>
        Check out more <nuxt-link to="/restaurants">restaurants</nuxt-link>!
      </AppToast>
    </section>

    <section class="options">
      <h3>Descriptions</h3>
      <p>{{ currentItem.description }}</p>
    </section>
  </main>
</template>

<script>
import { mapState } from 'vuex';
import AppToast from "@/components/AppToast";

export default {
  components: {
    AppToast,
  },
  data() {
    return {
      id: this.$route.params.id,
      quantity: 1,
      selectedAddOns: [],
      selectedOption: "",
      cartSubmitted: false
    }
  },
  computed: {
    ...mapState([
      'fooddata'
    ]),
    currentItem() {
      // use for loop for efficiency
      let result;

      for (let i = 0; i < this.fooddata.length; i++) {
        for (let j = 0; j < this.fooddata[i].menu.length; j++) {
          if (this.fooddata[i].menu[j].id === this.id) {
            result = this.fooddata[i].menu[j];
            break;
          }
        }
      }
      return result;
    },
    total() {
      const calculated = this.currentItem.price * this.quantity;
      return calculated.toFixed(2);
    }
  },
  methods: {
    addToCart() {
      let formOutput = {
        item: this.currentItem,
        quantity: this.quantity,
        option: this.selectedOption,
        addOns: this.selectedAddOns,
        total: this.total
      }

      this.cartSubmitted = true;
    }
  }
}
</script>

<style scoped>
.container {
  width: 1000px;
  margin: 100px auto;
  display: grid;
  grid-template-columns: 400px 1fr;
  grid-template-rows: 400px 1fr;
  grid-column-gap: 60px;
  grid-row-gap: 60px;
  line-height: 2;
}

.image {
  grid-area: 1 / 1 / 2 / 2;
  background-size: cover;
}

.details {
  grid-area: 1 / 2 / 2 / 3;
  position: relative;
}

.options {
  grid-area: 2 / 1 / 3 / 2;
}
</style>
