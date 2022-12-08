<template>
  <div>
    <AppHeader :count="numberOfItems" />

    <Carrito :items="items" :total="total" />

    <!-- <app-footer /> -->
    <AppFooter :isMobile="!isDesktop" :submenu="menu" />
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import Carrito from "./components/Carrito.vue";

const API_URL =
  "https://raw.githubusercontent.com/ironhack-jc/mid-term-api/main/cart";

export default {
  components: {
    AppHeader,
    AppFooter,
    Carrito,
  },
  data() {
    return {
      items: [],
      isDesktop: true,
      menu: ["Productos", "Servicios", "Contacta"],
    };
  },
  computed: {
    numberOfItems() {
      let sum = 0;

      for (const item of this.items) {
        sum += item.quantity;
      }

      return sum;
    },
    total() {
      /**
      let sum = 0;

      for (let index = 0; index < this.items.length; ++index) {
        const item = this.items[index];
        sum += item.price * item.quantity;
      }

      for (let index = 0; index < this.items.length; ++index) {        
        sum += this.items[index].price * this.items[index].quantity;
      }

      this.items.forEach(function (item) {
        sum += item.price * item.quantity;
      });

      this.items.forEach((item) => {
        sum += item.price * item.quantity;
      });

      for (const item of this.items) {
        sum += item.price * item.quantity;
      }

      return this.items.reduce(function (accumulator, item) {
        return accumulator + item.price * item.quantity;
      }, 0);

      return sum;
       */

      /** 
      return this.items.reduce(
        (accumulator, item) => accumulator + item.price * item.quantity,
        0
      );
      */

      return this.items.reduce(function (accumulator, item) {
        return accumulator + item.price * item.quantity;
      }, 0);
    },
  },
  methods: {
    async fetchApi() {
      const response = await fetch(API_URL);
      this.items = await response.json();
    },
    priceLine(item) {
      return item.price * item.quantity;
    },
    validateForm() {
      alert(`Hola`);
    },
    /**
     * Decrement the quantity by one but with a min of 0
     */
    decrementQuantity(item) {
      if (item.quantity > 0) {
        --item.quantity;
      }
    },
  },
  mounted() {
    this.fetchApi();
  },
};
</script>

<style scoped>
table {
  width: 100%;
}
table tfoot tr th {
  text-align: right;
}
</style>
