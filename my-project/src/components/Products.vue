<template>
  <button @click="toggleCartVisibility">Show Cart</button>
  <div v-if="showCart">
    <h2>Cart:</h2>
    <ul>
      <li v-for="(item, index) in cart" :key="index">{{ item }}</li>
    </ul>
  </div>

  <div class="flex justify-center gap-7 mt-3">
    <CategoryFilter @chosenCategory="getChosenCategoryFromChild" />
    <button @click.prevent="getFilteredProducts">Filter</button>
  </div>
  <button @click.prevent="toggleDisplayMode">Toggle Display</button>

  <div class="mx-12">
    <!-- <button type="button" @click="getProducts">show products</button> -->
  </div>
  <div
    class="grid"
    :class="[displayMode === 'grid4' ? 'grid-cols-4' : 'grid-cols-2']"
    id="generalProducts"
    v-if="!showCategorizedProducts"
  >
    <div
      v-for="(product, index) in products"
      :key="product.id"
      class="h-112 p-10 relative group"
    >
      <div class="image-container group-hover:hidden">
        <img
          :src="product.image"
          :alt="product.category"
          class="h-112 p-10 object-cover"
        />
      </div>

      <div
        class="absolute inset-0 p-10 hidden group-hover:block bg-white rounded-lg overflow-hidden"
        id="generalProductInformation"
        :style="
          displayMode === 'grid4' ? 'max-height: 300px; overflow-y: auto;' : ''
        "
      >
        <h4 class="text-xl font-bold">{{ product.title }}</h4>
        <p
          class="mt-2 text-xs font-light"
          :style="
            displayMode === 'grid4'
              ? 'max-height: 200px; overflow-y: auto; '
              : ''
          "
        >
          {{ product.description }}
        </p>
        <p class="mt-2 font-bold">Price: ${{ product.price }}</p>
        <button @click="addToCart(product)">Buy</button>
      </div>
    </div>
  </div>
  <div
    class="grid grid-cols-2 gap-4 justify-center px-28"
    id="categorizedProducts"
    v-if="showCategorizedProducts"
  >
    <div
      v-if="getFilteredProducts"
      v-for="(filteredProduct, index) in filteredProducts"
      :key="index"
      class="h-112 p-10 relative group"
    >
      <img
        :src="filteredProduct.image"
        :alt="filteredProduct.category"
        class="h-112 p-10 group-hover:hidden"
      />

      <div class="absolute inset-0 p-10 hidden group-hover:block">
        <h4 class="text-xl font-bold">{{ filteredProduct.title }}</h4>
        <p class="mt-2">{{ filteredProduct.description }}</p>
        <p class="mt-2 font-bold">Price: ${{ filteredProduct.price }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import CategoryFilter from "./CategoryFilter.vue";
export default {
  name: "Products",
  components: { CategoryFilter },
  data() {
    return {
      products: "",
      filteredProducts: [],
      chosenCategory: "",
      showCategorizedProducts: false,
      displayMode: "grid4",
      cart: [],
      showCart: false,
    };
  },
  mounted() {
    this.getProducts();
  },

  methods: {
    async getProducts() {
      //const randomNumber = Math.floor(Math.random() * 20) + 1;
      //const response = await fetch(`https://fakestoreapi.com/${randomNumber}`);
      const response = await fetch("https://fakestoreapi.com/products");
      const data = await response.json();
      this.products = data;
      this.$emit("sendProductsToApp", this.products);
    },

    getChosenCategoryFromChild(childCategory) {
      this.chosenCategory = childCategory;
    },

    getFilteredProducts() {
      //console.log(this.chosenCategory);
      this.filteredProducts = this.products.filter((product) => {
        return product.category === this.chosenCategory;
      });
      //console.log(this.filteredProducts);
      this.showCategorizedProducts = true;
      return this.filteredProducts;
    },
    toggleDisplayMode() {
      this.displayMode = this.displayMode === "grid4" ? "grid2" : "grid4";
    },
  },
  addToCart(product) {
    this.cart.push(product.title);
  },
  toggleCartVisibility() {
    this.showCart = !this.showCart;
  },
};
</script>

<style>
.read-the-docs {
  color: #888;
}
</style>
