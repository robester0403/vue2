<template>
  <div id="app">
    <Product :member="member" />
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
    };
  },
};
</script>
