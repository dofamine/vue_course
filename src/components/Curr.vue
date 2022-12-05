<template>
  {{ dollar(amt) }}
</template>

<script>
export default {
  props: ["amt"],
  name: "app-currency",
  methods: {
    dollar(value) {
      return "$" + Number.parseFloat(value).toFixed(2);
    },
  },
};
</script>

<style scoped></style>
