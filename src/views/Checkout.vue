<template>
  <div class="container">
    <h1>Checkout</h1>

    <table class="table table-hover">
      <caption class="text-right h3">
        <b>Total: </b>
        <app-currency :amt="total" />
      </caption>
      <thead>
        <tr>
          <th scope="col"></th>
          <th scope="col">Item</th>
          <th scope="col" class="text-center">Qty</th>
          <th scope="col" class="text-right">Price</th>
          <th scope="col" class="text-right">Sub-total</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product of model" :key="product.id">
          <td class="text-center">
            <div class="btn-group" role="group" aria-label="Basic example">
              <button
                @click="this.$emit('addToCart', product)"
                class="btn btn-success"
              >
                +
              </button>
              <button
                @click="this.$emit('remove', product)"
                class="btn btn-outline-success"
              >
                -
              </button>
            </div>
          </td>
          <th scope="row">{{ product.name }}</th>
          <td class="text-center">{{ product.qty }}</td>
          <td class="text-right"><app-currency :amt="product.price" /></td>
          <td class="text-right">
            <app-currency :amt="product.qty * product.price" />
          </td>
        </tr>
      </tbody>
    </table>
    <router-link class="btn btn-sm btn-success" to="/"
      >Keep Shopping</router-link
    >
  </div>
</template>

<script>
import AppCurrency from "@/components/Curr.vue";

export default {
  name: "app-checkout",
  components: { AppCurrency },
  props: ["model"],
  emits: ["addToCart", "remove"],
  computed: {
    total() {
      return this.model.reduce(
        (acc, product) => acc + product.price * product.qty,
        0
      );
    },
  },
  created() {
    this.emptyCartHandler();
  },
  watch: {
    model: {
      handler() {
        this.emptyCartHandler();
      },
      deep: true,
    },
  },
  methods: {
    emptyCartHandler() {
      if (!this.total) {
        this.$router.push("/");
      }
    },
  },
};
</script>

<style scoped></style>
