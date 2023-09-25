<template>
  <div>
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320">
      <path
        fill="#273036"
        fill-opacity="1"
        d="M0,96L80,117.3C160,139,320,181,480,176C640,171,800,117,960,96C1120,75,1280,85,1360,90.7L1440,96L1440,0L1360,0C1280,0,1120,0,960,0C800,0,640,0,480,0C320,0,160,0,80,0L0,0Z"
      ></path>
    </svg>
    <Cart :productsToAddInCart="arrOfDesiredProducts" />
    <h1
      class="text-center -mt-40 font-bold text-6xl from-stone-900 text-black drop-shadow-2xl"
    >
      THE SHOP
    </h1>
  </div>

  <!-- <Products @sendProductsToApp="getProductsFromChild" /> -->
  <Products @ArrayOfProductsToBuy="addDesiredProducts" />
</template>

<script>
import Products from "./components/Products.vue";
import Cart from "./components/Cart.vue";

export default {
  name: "App",
  components: { Products, Cart },

  data() {
    return {
      products: [],
      arrOfDesiredProducts: [],
    };
  },

  methods: {
    addDesiredProducts(product) {
      this.arrOfDesiredProducts.push(product);
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
