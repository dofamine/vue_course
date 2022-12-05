<template>
  <div class="col-2 m-auto">
    <button @click="$emit('addToCart', item)" class="btn btn-success">+</button>
  </div>
  <div class="col-sm-4">
    <img class="img-fluid d-block" :src="item.image" :alt="item.name" />
  </div>
  <div class="col">
    <h3 class="text-primary">{{ item.name }}</h3>
    <p class="mb-0">{{ item.description }}</p>
    <div class="h5 float-right">
      <span class="label"></span><app-currency :amt="item.price"></app-currency>
    </div>
  </div>
</template>

<script>
import AppCurrency from "@/components/Curr.vue";

export default {
  components: { AppCurrency },
  props: ["item"],
  emits: ["addToCart"],
  name: "app-product",
};
</script>

<style scoped></style>
