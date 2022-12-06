<template>
  <transition-group name="products" appear>
    <div
      v-for="item in products"
      :key="item.id"
      id="item-list"
      class="row align-items-center"
    >
      <app-product :item="item" @add-to-cart="addToCart"></app-product>
    </div>
  </transition-group>
</template>

<script>
import AppProduct from "@/components/Product.vue";

export default {
  name: "app-productList",
  components: { AppProduct },
  props: ["products"],
  emits: ["add-to-cart"],
  methods: {
    addToCart(item) {
      this.$emit("add-to-cart", item);
    },
  },
};
</script>

<style scoped lang="scss">
.products-enter-active,
.products-leave-active {
  transition: all 0.5s ease-in-out;
}

.products-enter-from {
  opacity: 0;
  transform: translateX(300px);
}

.products-leave-to {
  opacity: 0;
  transform: translateX(-300px);
}
</style>
