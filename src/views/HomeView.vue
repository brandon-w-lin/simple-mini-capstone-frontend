<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      display: false,
      products: [],
      createProductParams: {},
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
    createProduct: function () {
      // var params = {
      //   name: "abcde",
      //   description: "test description",
      //   image_url: "https://dynaimage.cdn.cnn.com/cnn/digital-images/org/98224ac3-aedc-44d4-9ad2-a6b8b0c06e2c.jpg",
      //   price: 5,
      // };

      var params = {
        name: this.createProductParams.name,
        description: this.createProductParams.description,
        image_url: this.createProductParams.image_url,
        price: this.createProductParams.price,
      };

      axios.post("http://localhost:3000/products.json", params).then((response) => {
        this.products.push(response.data);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <div>
      name:
      <input type="text" v-model="createProductParams.name" placeholder="name" />
      description:
      <input type="text" v-model="createProductParams.description" placeholder="description" />
      image_url:
      <input type="text" v-model="createProductParams.image_url" placeholder="image_url" />
      price:
      <input type="number" v-model="createProductParams.price" placeholder="price" />

      <button v-on:click="createProduct()">create a product</button>
    </div>
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
