<script>
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      display: false,
      products: [
        { id: 1, name: "Pillow", price: 25 },
        { id: 2, name: "Chair", price: 100 },
      ],
    };
  },
  created: function () {},
  methods: {},
};
</script>

<template>
  <div class="home">
    <p v-for="product in products" :key="product.id">{{ product.name }}</p>
  </div>
</template>

<style></style>
