<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>

  <Products @sendProductsToApp="getProductsFromChild" />
</template>

<script>
import Products from "./components/Products.vue";
import CategoryFilter from "./components/CategoryFilter.vue";

export default {
  name: "App",
  components: { Products },

  data() {
    return {
      products: [],
    };
  },

  methods: {
    getProductsFromChild(fetchedProducts) {
      this.products = fetchedProducts;
    },
  },
};
</script>

<style>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
