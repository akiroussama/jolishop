<template>
  <div class="ui cards" style="margin: 10px">
    <div class="ui icon input" style="width: 100%">
      <input type="text" placeholder="Search..." v-model="searchQuery" />
      <i class="search icon"></i>
    </div>
    <div class="card ui fluid" v-for="product in searchedProducts" :key="product.id" style="margin: 0">
      <div class="content">
        <img class="right floated mini ui image" :src="product.imageURL" />
  
        <div class="header">{{ product.name }}</div>
        <!-- <div class="meta">
                                                    {{ product.upc }} | {{ product.weight }} Kg |
                                                    {{ product.itemsperpack }} pack
                                                  </div> -->
      </div>
    </div>
  </div>
</template>

<script>
import { computed, onMounted, reactive, ref } from "vue";
export default {
  setup() {
    const products = reactive([]);
    const searchQuery = ref("");

    const searchedProducts = computed(async () => {
      const apiBaseUrl = 'https://thawing-scrubland-03171.herokuapp.com/https://skincare-api.herokuapp.com/';
      const searchProduct = 'product?q=';
      const product = 'ciracle';
      const res = await fetch(apiBaseUrl + searchProduct + product);
      if (res.ok) {
        const productsSnap = await res.json();
        productsSnap.forEach((doc) => {
          let product = {};
          product.id = doc.id;
          product.name = doc.name;
          product.brand = doc.brand;
          product.imageURL = doc.imageURL || '';
          products.push(product);
        });
      } else {
        alert('error fetching');
      }
      return products;
    });
    onMounted(async () => {
      console.log('mounted')
    });
    return { searchedProducts, searchQuery };
  },
};
</script>