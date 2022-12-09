<template>
  <div class="dropdown-clip" v-if="items.length > 0">
    <transition name="dropdown">
      <div v-if="show" class="list-group" aria-labelledby="cartDropdown">
        <div
          v-for="(item, index) in items"
          :key="index"
          class="list-group-item d-flex justify-content-end align-items-center"
        >
          <div>
            {{ item.name }}
            <strong>{{ item.qty > 1 ? `x ${item.qty}` : "" }}</strong>
          </div>
          <div class="price">
            <app-currency :amt="item.price"></app-currency>
          </div>
          <button
            @click.self.stop="this.$emit('onDelete', item)"
            class="btn btn-danger btn-sm"
          >
            -
          </button>
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
  emits: ["onDelete"],
  name: "app-dropdown",
};
</script>

<style scoped lang="scss">
.price {
  margin-left: 5px;
  font-weight: bold;
  color: green;
}

.btn-danger {
  margin-left: 5px;
}

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
