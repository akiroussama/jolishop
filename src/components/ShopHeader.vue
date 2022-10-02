<script setup>
const apiBaseUrl = 'https://thawing-scrubland-03171.herokuapp.com/https://skincare-api.herokuapp.com/';
const searchProduct = 'product?q=';
const product = 'ciracle';
const res = await fetch(apiBaseUrl + searchProduct + product);
if (res.ok) {
  const data = await res.json();
  console.log(data);
}
</script>

<template>
  <h1>Shop Header</h1>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
