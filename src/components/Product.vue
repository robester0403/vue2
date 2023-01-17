<template>
  <div>
    <header id="header">
      <div class="container">
        <div class="cart">
          <p><i class="fas fa-shopping-cart" /> {{ cart }}</p>
        </div>
      </div>
    </header>
    <div class="container">
      <div class="product">
        <div class="image"><img v-bind:src="productImage" alt="product" /></div>
        <div class="content">
          <h1>{{ title }}</h1>
          <div class="stockinfo">
            <span class="green" v-if="{ inStock }">In Stock</span>
            <span class="amber" v-else-if="inventory > 0">Low Stock</span>
            <span class="red" v-else>Out of Stock</span>
          </div>
          <ul class="features">
            <li v-for="(feature, index) in features" :key="index">
              {{ feature }}
            </li>
          </ul>
          <div class="variants">
            <span
              v-for="(variant, index) in variants"
              :key="variant.variantId"
              @mouseover="updateImage(index)"
              class="colorBox"
              :style="{ backgroundColor: variant.variantColor }"
            />

            <div class="addCart">
              <button
                v-on:click="addToCart"
                :disabled="inventory <= 0"
                :class="{ disabledState: inventory <= 0 }"
              >
                Add to Cart
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Product",
  inStock() {
    return this.inventory > 50;
  },
  data() {
    return {
      brand: "Nike",
      product: "Air Force",
      selectedVariant: 0,
      inventory: 10,
      cart: 0,
      features: ["Durable Leather", "Comfortable", "Lightweight"],
      variants: [
        {
          variantId: 1,
          variantColor: "red",
          variantImage: require("../assets/images/nike-red.jpg"),
          variantQty: 20,
        },
        {
          variantId: 2,
          variantColor: "white",
          variantImage: require("../assets/images/nike-white.jpg"),
          variantQty: 5,
        },
        {
          variantId: 3,
          variantColor: "Black",
          variantImage: require("../assets/images/nike-black.jpg"),
          variantQty: 0,
        },
      ],
    };
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
    updateImage(index) {
      this.selectedVariant = index;
      console.log(index);
    },
  },
  computed: {
    title() {
      return `${this.brand} ${this.product}`;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
