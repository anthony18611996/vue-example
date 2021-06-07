<template>
  <div class="row">
    <div class="col-lg-6">
      <div class="product d-flex flex-wrap">
        <div class="product-image mx-auto">
          <img :src="image" alt="" />
        </div>
        <div class="product-info mx-auto text-center">
          <h1>{{ title }}</h1>
          <p v-if="inStock">In stock</p>
          <p v-else-if="inventory <= 10 && inventory > 0">Almost</p>
          <p v-else>Out of stock</p>
          <p>Shipping: {{ shipping }}</p>
        </div>
      </div>
    </div>
    <div class="col-lg-6">
      <ul class="mt-5">
        <li v-for="detail in details" :key="detail.id">
          {{ detail }}
        </li>
      </ul>
      <div
        class="variables color-box"
        v-for="(variant, index) in variants"
        :key="variant.variantId"
        :style="{ backgroundColor: variant.variantColor }"
        @mouseover="updateProduct(index)"
      ></div>
      <button
        :class="{ disabledButton: !inStock }"
        @click="addToCart"
        :disabled="!inStock"
      >
        Add to Cart
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "product",
  components: {},
  props: {
    premium: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      cart: 0,
      brand: "Vue Mastery",
      product: "Socks",
      selectedVariant: 0,
      inventory: 8,
      details: ["80% Sirk", "20% Tina", "Gender-natural"],
      variants: [
        {
          variantId: 228,
          variantColor: "green",
          variantImage: require(`@/assets/h1.jpg`),
          variantQuantity: 10,
        },
        {
          variantId: 1488,
          variantColor: "blue",
          variantImage: require(`@/assets/h2.jpg`),
          variantQuantity: 0,
        },
      ],
    };
  },
  methods: {
    addToCart() {
      this.$emit("add-to-cart", this.variants[this.selectedVariant].variantId);
    },
    updateProduct(index) {
      this.selectedVariant = index;
    },
  },
  computed: {
    title() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    },
    shipping() {
      if (this.premium) {
        return "Free";
      }
      return 2.99;
    },
  },
};
</script>
