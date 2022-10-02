<script>
import debounce from "lodash.debounce";
export default {
    data() {
        return {
            searchBrand: '',
            filteredProducts: 'Products usually contain a Product mark. ;-)',
            isDisabled: false,
        }
    },
    created() {
        this.debouncedWatch = debounce((newProduct, oldProduct) => {
            this.getFiltredProduct()
        }, 500);
    },
    watch: {
        // whenever Product changes, this function will run
        searchBrand(...args) {
            this.debouncedWatch(...args);

        }
    },
    beforeUnmount() {
        this.debouncedWatch.cancel();
    },
    methods: {
        async getFiltredProduct() {
            this.filteredProducts = 'loading...'
            try {
                // disable the input waiting the response
                this.isDisabled = true;
                const apiBaseUrl = 'https://thawing-scrubland-03171.herokuapp.com/https://skincare-api.herokuapp.com/product?q=';
                const res = await fetch(apiBaseUrl + this.searchBrand);
                this.filteredProducts = (await res.json());
                this.isDisabled = false;
            } catch (error) {
                this.isDisabled = false;
                this.filteredProducts = 'Error! Could not reach the API. ' + error
            }
        }
    }
}
</script>
    
<template>
    <div class="app">
        <div class="app-wrapper">
            <div class="search-bar">
                <h2>Search items</h2>
                <input id="search" v-model="searchBrand" type="search" class="search" placeholder="start typing"
                    :disabled=isDisabled />
            </div>
            <div class="items-wrapper" id="items-wrapper">
                <div v-if="filteredProducts.length === 0" class="no-items">
                    <p>No items found</p>
                </div>
                <div v-else class="items">
                    <div v-for="product in filteredProducts" :key="product.id" class="item">
                        <div class="item-info">
                            <h3>{{product.name}}</h3>
                            <p>{{product.brand}}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style>
:root {
    font-size: 8px;
}

@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;700&display=swap");

body {
    background-color: #ffffff;
}

.items {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin-top: 2rem;
}

h1 {
    font-family: "Montserrat", sans-serif;
    font-size: 3rem;
    font-weight: 500;
    letter-spacing: 2%;
    line-height: 30px;
    color: #464141;
}

h2 {
    font-family: "Montserrat", sans-serif;
    font-size: 2.5rem;
    font-weight: 500;
    letter-spacing: 2%;
    line-height: 24px;
    color: #464141;
}

p {
    font-family: "Montserrat", sans-serif;
    font-size: 2rem;
    font-weight: weight(regular);
    letter-spacing: 2%;
    line-height: 20px;
    color: #a2a4aa;
}

.app {
    margin: auto;
    width: 100%;
    max-width: 1048px;
}

.app-warpper {
    margin: auto;
}

.search-bar {
    text-align: center;
    margin-top: 4rem;
}

.search-bar input {
    padding: 2rem;
    min-width: 40rem;
}

.items-wrapper {
    margin-top: 40px;
    display: flex;
    justify-content: flex-start;
    flex-wrap: wrap;
}

/* item card */
.item-card {
    min-width: 160px;
    min-height: 180px;
    background-color: #f6f6f6;
    border-radius: 7px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: 0 10px 10px 0;
}

.item-card__icon-circle {
    background-color: #fffcfc;
    width: 85px;
    height: 85px;
    border-radius: 50%;
    margin: 0 auto 0 auto;
    display: flex;
    justify-content: center;
    align-items: center;
}

.item-card__icon-circle img {
    max-width: 60px;
    max-height: 60px;
    object-fit: contain;
}

.item-card__variety {
    color: #464141;
    text-align: center;
    margin: 15px auto 0 auto;
    text-transform: lowercase;
    text-transform: capitalize;
}

.item-card__title {
    font-weight: 500;
    color: #464141;
    margin: 15px auto 15px auto;
    text-transform: lowercase;
    text-transform: capitalize;
}

.item-card__code {
    color: #36b16c;
    margin: 15px auto 0 auto;
}
</style>