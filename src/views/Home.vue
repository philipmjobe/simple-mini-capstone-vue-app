<template>
  <div class="home">
    <h1>
      <u>{{ message }}</u>
    </h1>
    <div v-for="product in products" v-bind:key="product.id">
      <h3>{{ product.name }}</h3>
      <p>{{ product.price }}</p>
    </div>
  </div>
</template>

<style></style>

<script>
const axios = require("axios");
export default {
  data: function () {
    return {
      message: "Welcome to the end!",
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("http://localhost:3000/products").then((response) => {
        this.products = response.data;
      });
    },
  },
};
</script>
