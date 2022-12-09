<template>
  <div
    :class="[
      type ? 'alert-' + type : 'alert-secondary',
      close ? 'alert-dismissible' : '',
    ]"
    class="alert"
    role="alert"
    ref="alert"
  >
    <slot>Congrats on getting some items in your cart.</slot>
    <button
      v-if="close"
      @click="closeButton($event)"
      type="button"
      class="btn-close"
      aria-label="Close"
    ></button>
  </div>
</template>

<script>
export default {
  props: ["type", "close"],
  methods: {
    closeButton(event) {
      event.target.parentNode.remove();
    },
  },
  mounted() {
    setTimeout(() => {
      this.$refs.alert && this.$refs.alert.remove(), 2000;
    });
  },
  name: "app-alert",
};
</script>

<style scoped></style>
