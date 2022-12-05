<template>
  <div
    :class="[
      type ? 'alert-' + type : 'alert-secondary',
      close ? 'alert-dismissible' : '',
    ]"
    class="alert"
    role="alert"
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
  name: "app-alert",
};
</script>

<style scoped></style>
