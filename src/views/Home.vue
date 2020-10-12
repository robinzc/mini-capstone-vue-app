<template>
  <div class="home">
    <div>
      <h2>New Product</h2>
      <button v-on:click="createProduct">Create product</button>
    </div>
    <h1>Products!</h1>
    <div v-for="product in products">
      <h2>Name: {{ product.name }}</h2>
      <h4>Description: {{ product.description }}</h4>
      <h5>Price: {{ product.price }}</h5>
    </div>
  </div>
</template>
<style></style>
<script>
import axios from "axios";

export default {
  data: function() {
    return {
      products: [],
    };
  },
  created: function() {
    this.indexProducts();
  },
  methods: {
    indexProducts: function() {
      axios.get("/api/products").then((response) => {
        console.log(response.data);
        this.products = response.data;
      });
    },
    createProduct: function() {
      var params = {
        name: "Example name",
        description: "Example description",
        price: "Example price",
      };

      axios
        .post("/api/products", params)
        .then((response) => {
          console.log("Success", response.data);
          this.recipes.push(response.data);
        })
        .catch((error) => {
          console.log(error.response);
        });
    },
  },
};
</script>
