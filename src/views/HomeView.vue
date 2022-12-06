<template>
  <section class="container">
    <app-range-select
      v-model="max"
      :shown-products-amt="filteredProducts.length"
    ></app-range-select>

    <app-alert v-if="model.length" type="success" :close="true"></app-alert>

    <app-productList
      :products="filteredProducts"
      @add-to-cart="addToCart"
    ></app-productList>
  </section>
</template>

<script>
import { defineComponent } from "vue";
import AppAlert from "@/components/Alert.vue";
import AppProductList from "@/components/ProductList.vue";
import AppRangeSelect from "@/components/RangeSelect.vue";

export default defineComponent({
  name: "app-home",
  emits: ["add-to-cart"],
  props: ["model"],
  components: {
    AppAlert,
    AppRangeSelect,
    AppProductList,
  },
  data() {
    return {
      max: 50,
      products: [],
    };
  },
  created() {
    fetch("https://hplussport.com/api/products/order/price")
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
      });
  },
  methods: {
    addToCart(product) {
      this.$emit("add-to-cart", product);
    },
  },
  computed: {
    filteredProducts() {
      return this.products.filter(
        (item) => Number(item.price) < Number(this.max)
      );
    },
  },
});
</script>
