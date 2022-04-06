<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      display: false,
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("http://localhost:3000/products.json").then((response) => {
        this.products = response.data;
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <div v-for="product in products" :key="product.id">
      <div class="productBlock">
        <h1>
          {{ product.name }}
        </h1>
        <br />
        <img v-bind:src="product.image_url" v-bind:alt="product.name" class="productImage" />
      </div>
    </div>
  </div>
</template>

<style>
.productBlock {
  border-style: solid;
  border-color: black;
  display: inline-block;
  width: 500px;
  padding: 10px;
  margin: 10px;
}

.productImage {
  width: 300px;
}
</style>
