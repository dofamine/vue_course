<template>
  <nav class="navbar navbar-light sticky-top mr-3">
    <div
      v-if="cartState.length"
      class="w-100 navbar-text ml-auto d-flex justify-content-end position-relative"
    >
      <div
        class="mr-auto d-flex align-items-end flex-column bd-highlight mb-3 position-absolute"
      >
        <div class="mb-2">
          <span class="cart-total"><app-currency :amt="cartTotal" /></span>
          <button
            @click="displayCart = !displayCart"
            class="btn btn-sm btn-success ml-3"
            id="cartDropdown"
            aria-haspopup="true"
            aria-expanded="false"
          >
            <font-awesome-icon
              icon="fa-solid fa-shopping-cart"
            ></font-awesome-icon>
            {{ itemsInCart }}
          </button>
        </div>
        <app-dropdown :show="displayCart" :items="cartState"></app-dropdown>
      </div>
    </div>
  </nav>
</template>

<script>
import AppCurrency from "@/components/Curr.vue";
import AppDropdown from "@/components/Dropdown.vue";

export default {
  name: "app-navbar",
  props: ["cartState"],
  components: { AppDropdown, AppCurrency },
  data() {
    return {
      displayCart: true,
    };
  },
  computed: {
    cartTotal() {
      return this.cartState.reduce(
        (inc, item) => Number(item.price) * item.qty + inc,
        0
      );
    },
    itemsInCart() {
      return this.cartState.reduce((acc, item) => acc + item.qty, 0);
    },
  },
};
</script>

<style scoped>
.cart-total {
  font-weight: bold;
  margin-right: 10px;
  color: green;
}
</style>
