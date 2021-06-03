<template>
  <link
    rel="stylesheet"
    href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css"
    integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm"
    crossorigin="anonymous"
  />
  <div class="nav-bar mb-5"></div>
  <div class="container">
    <div class="row">
      <div class="col-lg-6">
        <div class="product d-flex flex-wrap">
          <div class="product-image mx-auto">
            <img :src="image" alt="" />
          </div>
          <div class="product-info mx-auto text-center">
            <h1>{{ kris }}</h1>
            <p v-if="inStock">In stock</p>
            <p v-else-if="inventory <= 10 && inventory > 0">Almost</p>
            <p v-else>Out of stock</p>
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
          class="variables"
          v-for="variant in variants"
          :key="variant.variantId"
        >
          <p
            @mouseover="updateProduct(variant.variantImage)"
            style="cursor: pointer"
          >
            {{ variant.variantColor }}
          </p>
        </div>
        <div class="cart d-flex">
          <button @click="addToCart">Add to Cart</button>
          <div class="cart__count ml-3">
            <p>Cart ({{ cart }})</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      kris: "Kris Tina",
      image: require(`@/assets/kris.jpg`),
      inStock: true, //помнять на false, чтобы показать другие условия
      inventory: 8,
      details: ["80% Kris", "20% Tina", "Gender-natural"],
      variants: [
        {
          variantId: 228,
          variantColor: "green",
          variantImage: require(`@/assets/kris.jpg`),
        },
        {
          variantId: 1488,
          variantColor: "blue",
          variantImage: require(`@/assets/kris2.jpg`),
        },
      ],
      cart: 0,
    };
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
    updateProduct(variantImage) {
      this.image = variantImage;
    },
  },
};
</script>

<style>
.nav-bar {
  background-color: aquamarine;
  height: 80px;
}

.product-image {
  max-width: 400px;
  max-height: 400px;
}

.product-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
body {
  min-height: 100vh;
}

li,
p {
  font-size: 20px;
  font-weight: 500;
}
</style>
