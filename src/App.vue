<template>
  <app-navbar :cartState="cartState"></app-navbar>
  <div class="container">
    <router-view :model="cartState" @add-to-cart="addToCart" />
  </div>
</template>

<script lang="ts">
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
    addToCart(product: any) {
      this.cartState.push(toRaw(product));
    },
  },
};
</script>

<style lang="scss">
@import "bootstrap";
</style>
