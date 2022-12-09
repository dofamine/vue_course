<template>
  <app-navbar
    :cartState="cartState"
    @onDelete="deleteProductFromCart"
  ></app-navbar>
  <div class="container">
    <router-view
      :model="cartState"
      @add-to-cart="addToCart"
      @remove="deleteProductFromCart"
    />
  </div>
</template>

<script>
import AppNavbar from "@/components/Navbar.vue";
import { toRaw } from "vue";

export default {
  components: {
    AppNavbar,
  },
  data() {
    return {
      cartState: [],
    };
  },
  methods: {
    addToCart(product) {
      let existingItem = this.cartState.find((item) => item.id === product.id);
      if (existingItem) {
        existingItem.qty++;
      } else {
        product.qty = 1;
        this.cartState.push(toRaw(product));
      }
    },
    deleteProductFromCart(product) {
      const productIndex = this.cartState.findIndex(
        (item) => item.id === product.id
      );
      if (this.cartState[productIndex].qty > 1) {
        this.cartState[productIndex].qty--;
      } else {
        this.cartState.splice(productIndex, 1);
      }
    },
  },
};
</script>

<style lang="scss">
@import "bootstrap";
</style>
