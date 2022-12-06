<template>
  <div class="dropdown-clip" v-if="items.length > 0">
    <transition name="dropdown">
      <div v-if="show" class="list-group" aria-labelledby="cartDropdown">
        <div
          v-for="(item, index) in items"
          :key="index"
          class="list-group-item d-flex justify-content-between"
        >
          <div>{{ item.name }}</div>
          <div class="ml-3 font-weight-bold">
            <app-currency :amt="item.price"></app-currency>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import AppCurrency from "@/components/Curr.vue";

export default {
  components: { AppCurrency },
  props: ["show", "items"],
  name: "app-dropdown",
};
</script>

<style scoped lang="scss">
.dropdown-clip {
  overflow: hidden;
}

.dropdown-enter-active,
.dropdown-leave-active {
  transition: all 0.5s ease-in-out;
  transform: auto;
}

.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: translateY(-300px);
}
</style>
