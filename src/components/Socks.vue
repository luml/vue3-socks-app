<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img :src="image" alt="sock image" />
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock > 10">In Stock</p>
        <p v-else-if="inStock <= 10 && inStock > 0">Almost Sold Out</p>
        <p v-else>Out of Stock</p>

        <p>Shipping: {{ shipping }}</p>

        <ul>
          <li v-for="detail in details" :key="detail">{{ detail }}</li>
        </ul>
        <div
          v-for="(variant, index) in variants"
          :key="variant.id"
          @mouseover="updateVariant(index)"
          class="color-circle"
          :style="{ backgroundColor: variant.color }"
        ></div>
        <button
          :disabled="!inStock"
          class="button"
          :class="{ disabledButton: !inStock }"
          @click="addToCard"
        >
          Add to Cart
        </button>
      </div>
    </div>
  </div>
  <review-list v-if="reviews.length" :reviews="reviews"></review-list>
  <review-form @review-submitted="addReview"></review-form>
  <!-- <base-vee-input></base-vee-input> -->
</template>

<script>
import ReviewForm from "./ReviewForm.vue";
import ReviewList from "./ReviewList.vue";
// import BaseVeeInput from "./BaseVeeInput.vue";
export default {
  name: "Socks",
  components: {
    ReviewForm,
    ReviewList,
    // BaseVeeInput
  },
  props: {
    premium: {
      type: Boolean,
      require: true,
    },
  },
  data() {
    return {
      product: "Socks",
      // TODO can't get images from assets
      selectedVariant: 0,
      url: "https://www.vuemastery.com/",
      description: "A warm fuzzy pair of socks.",
      // inStock: false,
      // inventory: 100,
      details: ["50% cotton", "30% wool", "20% polyester"],
      variants: [
        {
          id: 2234,
          color: "green",
          image: "/images/socks_green.jpg",
          quantity: 50,
        },
        {
          id: 2235,
          color: "blue",
          image: "/images/socks_blue.jpg",
          quantity: 0,
        },
      ],
      cart: 0,
      brand: "Vue Mastery",
      reviews: [],
    };
  },
  computed: {
    title() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].image;
    },
    inStock() {
      return this.variants[this.selectedVariant].quantity;
    },
    shipping() {
      if (this.premium) {
        return "free";
      } else {
        return "$2.99";
      }
    },
  },
  methods: {
    addToCard() {
      this.$emit("add-to-cart", this.variants[this.selectedVariant].id);
    },
    updateVariant(index) {
      this.selectedVariant = index;
    },
    addReview(review) {
      this.reviews.push(review);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
