<template>
  <link
    rel="stylesheet"
    href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css"
    integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm"
    crossorigin="anonymous"
  />
  <div class="nav-bar mb-5"></div>
  <div class="container">
    <div class="cart d-flex">
      <div class="cart__count ml-3">
        <p>Cart ({{ cart.length }})</p>
      </div>
    </div>
    <product :premium="premium" @add-to-cart="updateCart" />
  </div>
</template>

<script>
import product from "@/components/product";

export default {
  name: "App",
  components: {
    product,
  },
  data() {
    return {
      cart: [],
    };
  },
  methods: {
    updateCart(id) {
      this.cart.push(id)
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
  min-height: 400px;
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

.color-box {
  width: 40px;
  height: 40px;
  margin-top: 10px;
  margin-bottom: 10px;
}

.disabledButton {
  background-color: #ebebeb;
  border: 1px solid red;
  color: red;
}
</style>
