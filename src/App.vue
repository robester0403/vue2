<template>
  <div>
    <header id="header">
      <div class="container">
        <div class="cart">
          <p><i class="fas fa-shopping-cart" /> {{ cart.length }}</p>
        </div>
      </div>
    </header>
    <div id="app">
      <Product :member="member" @addToCart="updatecart" />
    </div>
  </div>
</template>

<script>
import Product from "./components/Product.vue";

export default {
  name: "App",
  components: {
    Product,
  },
  data() {
    return {
      member: true,
      cart: [],
    };
  },
  methods: {
    updatecart(id) {
      this.cart = [...this.cart, id];
    },
  },
};
</script>
