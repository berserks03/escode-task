<template>
  <div class="app">
    <h1 class="app__title">Product Catalog</h1>
    <ProductList />
  </div>
</template>

<script setup>
import ProductList from './components/ProductList.vue'
</script>

<style scoped>
.app {
  padding: 20px;
  background-color: #f4f4f9;
  min-height: 100vh;
}

.app__title {
  font-size: 2.5rem;
  font-weight: bold;
  text-align: center;
  margin-bottom: 40px;
}
</style>
