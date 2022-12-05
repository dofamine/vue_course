<template>
  <nav class="navbar navbar-light sticky-top mr-3">
    <div
      v-if="cart.length"
      class="w-100 navbar-text ml-auto d-flex justify-content-end position-relative"
    >
      <div
        class="mr-auto d-flex align-items-end flex-column bd-highlight mb-3 position-absolute"
      >
        <div class="mb-2">
          <span class="font-weight-bold bg-white"
            ><app-currency :amt="cartTotal"
          /></span>
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
            {{ cart.length }}
          </button>
        </div>
        <div class="dropdown-clip">
          <transition name="dropdown">
            <div
              v-if="displayCart"
              class="list-group"
              aria-labelledby="cartDropdown"
            >
              <div
                v-for="(item, index) in cart"
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
      </div>
    </div>
  </nav>

  <section class="container">
    <label for="max-price" class="form-label h2">Max Price (${{ max }})</label>
    <div class="badge bg-success ml-3">
      results: {{ filteredProducts.length }}
    </div>

    <input
      v-model.number="max"
      type="range"
      class="form-range"
      min="0"
      max="130"
    />

    <app-alert type="danger" close="true" v-if="cartTotal > 100"> </app-alert>

    <transition-group name="products" appear>
      <div
        v-for="item in filteredProducts"
        :key="item.id"
        id="item-list"
        class="row align-items-center"
      >
        <app-product :item="item" @add-to-cart="addToCart"></app-product>
      </div>
    </transition-group>
  </section>
</template>

<script>
import { defineComponent } from "vue";
import AppAlert from "@/components/Alert.vue";
import AppCurrency from "@/components/Curr.vue";
import AppProduct from "@/components/Product.vue";

export default defineComponent({
  name: "app-home",
  components: {
    AppProduct,
    AppCurrency,
    AppAlert,
  },
  data() {
    return {
      max: 50,
      cart: [],
      displayCart: false,
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
  computed: {
    filteredProducts() {
      return this.products.filter((item) => item.price < this.max);
    },
    cartTotal() {
      return this.cart.reduce((inc, item) => Number(item.price) + inc, 0);
    },
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
      if (this.cartTotal >= 100) {
        this.salesBtn = "btn-danger";
      }
    },
  },
});
</script>
