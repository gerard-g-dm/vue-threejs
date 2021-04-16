<template>
  <div id="app">
    <product-list />
  </div>
</template>

<script>
import ProductList from "./views/product-list/product-list";

export default {
  name: "App",
  components: {
    ProductList
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
