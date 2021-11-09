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
export default {
  data: function () {
    return {
      message: "Welcome to the end!",
      products: [
        { id: 1, name: "Product 1", price: 10 },
        { id: 2, name: "Product 2", price: 230 },
      ],
    };
  },
  created: function () {},
  methods: {},
};
</script>
