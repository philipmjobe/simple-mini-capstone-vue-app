<template>
  <div class="home">
    <h1>
      <u>{{ message }}</u>
    </h1>
    <h2>New Product</h2>
    Name:
    <input type="text" v-model="newProductParams.name" />
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
      <button v-on:click="showProduct(product)">More Info</button>
    </div>
    <dialog id="product-details">
      <form method="dialog">
        <h1>Product Info:</h1>
        <p>
          Name:
          <input type="text" v-model="currentProduct.name" />
        </p>
        <p>
          Description:
          <input type="text" v-model="currentProduct.description" />
        </p>
        <p>
          Price:
          <input type="text" v-model="currentProduct.price" />
        </p>
        <p>
          Image Url:
          <input type="text" v-model="currentProduct.image_url" />
        </p>
        <button v-on:click="updateProduct(currentProduct)">Update Product</button>
        <button v-on:click="destroyProduct(currentProduct)">Delete</button>
        <button>close</button>
      </form>
    </dialog>
  </div>
</template>

<style>
#app {
  background-color: rgb(1, 6, 7);
  color: rgb(155, 25, 25);
}
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
      currentProduct: {},
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
          this.products.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
    showProduct: function (product) {
      console.log(product);
      this.currentProduct = product;
      document.querySelector("#product-details").showModal();
    },
    updateProduct: function (product) {
      axios.patch("http://localhost:3000/products/" + product.id, product).then((response) => {
        console.log("Sucess", response.data);
      });
    },
    destroyProduct: function (product) {
      axios.delete("http://localhost:3000/products/" + product.id).then((response) => {
        console.log("Sucess", response.data);
        var index = this.products.indexOf(product);
        this.products.splice(index, 1);
      });
    },
  },
};
</script>
