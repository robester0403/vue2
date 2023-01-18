<template>
  <div>
    <div class="container">
      <div class="product">
        <div class="image"><img v-bind:src="productImage" alt="product" /></div>
        <div class="content">
          <h1>{{ title }}</h1>
          <div class="stockinfo">
            <span class="green" v-if="inventory > 19">In Stock</span>
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
          <div class="shipping">Shipping: {{ shipping }}</div>
        </div>
      </div>
      <div class="reviews">
        <h2>Reviews</h2>
        <p v-if="!reviews.length">There are no reviews yet.</p>
        <ul>
          <li v-for="(review, index) in reviews" :key="index">
            <p>{{ review.name }}</p>
            <span
              >Rating: {{ review.rating }}, <strong>Review</strong>
              {{ review.review }}</span
            >
          </li>
        </ul>
        <ProductReview @review-submitted="addReview"> </ProductReview>
      </div>
      <ProductTabs />
    </div>
  </div>
</template>

<script>
import ProductReview from "./ProductReview.vue";
import ProductTabs from "./ProductTabs.vue";
export default {
  components: {
    ProductReview,
    ProductTabs,
  },
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Product",
  props: {
    member: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      brand: "Nike",
      product: "Air Force",
      selectedVariant: 0,
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
      reviews: [],
    };
  },
  methods: {
    addToCart() {
      this.$emit("addToCart", this.variants[this.selectedVariant].variantId);
    },
    updateImage(index) {
      this.selectedVariant = index;
    },
    addReview(productReview) {
      this.reviews = [...this.reviews, productReview];
    },
  },
  computed: {
    title() {
      return `${this.brand} ${this.product}`;
    },
    productImage() {
      return this.variants[this.selectedVariant].variantImage;
    },
    inventory() {
      return this.variants[this.selectedVariant].variantQty;
    },
    shipping() {
      if (this.member) {
        return "Included with Membership";
      }
      return "$2.99";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
