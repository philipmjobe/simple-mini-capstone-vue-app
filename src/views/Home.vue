<template>
  <div class="home">
    <h1>
      <u>{{ message }}</u>
    </h1>
    <h2>New Product</h2>
    Name:
    <input type="text" v-model="newProductParams.title" />
    Description:
    <input type="text" v-model="newProductParams.description" />
    Price:
    <input type="text," v-model="newProductParams.price" />
    Image Url:
    <input type="text" v-model="newProductParams.image_url" />
    <button v-on:click="createProduct()">Create Product</button>
    <div v-for="product in products" v-bind:key="product.id">
      <h3>{{ product.name }}</h3>
      <p>{{ product.price }}</p>
      <img :src="product.image_url" :alt="product.name" />
    </div>
  </div>
</template>

<style>
img {
  width: 250px;
}
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to the Shop!",
      products: [],
      newProductParams: {},
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
    createProduct: function () {
      console.log("Creating a new product");

      axios
        .post("http://localhost:3000/products", this.newProductParams)
        .then((response) => {
          console.log("Success", response.data);
          this.product.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
