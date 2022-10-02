<script setup>
import { ref } from 'vue';
// const header = ref('Shop Header');
// const items = ref([{ message: 'Foo' }, { message: 'Bar' }])
let input = ref("");
const apiBaseUrl = 'https://thawing-scrubland-03171.herokuapp.com/https://skincare-api.herokuapp.com/';
const searchProduct = 'product?q=';
const product = 'ciracle';

const res = await fetch(apiBaseUrl + searchProduct + product);
if (res.ok) {
  const fruits = await res.json();
  const productlist = ref(datas)

} else {

  const fruits = ["apple", "banana", "orange"];
}
function filteredList() {
  return fruits.filter((fruit) =>
    fruit.toLowerCase().includes(input.value.toLowerCase())
  );
}
</script>
<template>
  <input type="text" v-model="input" placeholder="Search fruits..." />
  <div class="item fruit" v-for="fruit in filteredList()" :key="fruit">
    <p>{{ fruit }}</p>
  </div>
  <div class="item error" v-if="input&&!filteredList().length">
    <p>No results found!</p>
  </div>
</template>
<!-- 
<template>
  <h1>{{ header }}</h1>

  <div class="post">

    <div v-if="productlist" class="content">
      <ul>
        <li v-for="item in productlistproductlist">
          {{ item.name }}
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
const apiBaseUrl = 'https://thawing-scrubland-03171.herokuapp.com/https://skincare-api.herokuapp.com/';
const searchProduct = 'product?q=';
const product = 'ciracle';

const res = await fetch(apiBaseUrl + searchProduct + product);
if (res.ok) {
  const datas = await res.json();
  const productlist = ref(datas)

}
</script> -->
