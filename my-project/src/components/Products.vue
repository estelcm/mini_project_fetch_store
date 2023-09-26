<template>
  <!-- <button @click="toggleCartVisibility">Show Cart</button>
  <div v-if="showCart">
    <h2>Cart:</h2>
    <ul>
      <li v-for="(item, index) in cart" :key="index">{{ item }}</li>
    </ul>
  </div> -->

  <div class="flex justify-center items-center gap-7 mt-3">
    <CategoryFilter
      @chosenCategory="getChosenCategoryFromChild"
      class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
    />
    <button
      @click.prevent="getFilteredProducts"
      class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
    >
      Filter
    </button>
    <button
      @click.prevent="toggleDisplayMode"
      class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
    >
      Display
    </button>
  </div>
  <div class="flex flex-row-reverse justify-items-end mr-20"></div>

  <div class="mx-12">
    <!-- <button type="button" @click="getProducts">show products</button> -->
  </div>
  <!-- ALL CATEGORIES SECTION SHOWN BY DEFAULT -->
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
        <h6 class="text-xl font-bold">{{ product.title }}</h6>
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
        <button
          @click="addToCart(product.id)"
          class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
        >
          Buy
        </button>
      </div>
    </div>
  </div>
  <!-- FILTERED CATEGORIES SHOWN -->
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
        class="h-112 p-10 group-hover:hidden image-container"
      />

      <div class="absolute inset-0 p-10 hidden group-hover:block">
        <h6 class="text-xl font-bold">{{ filteredProduct.title }}</h6>
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
      productsCart: [],
      showCart: false,
      cartItem: "",
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
      if (this.chosenCategory === "all Categories") {
        return (this.filteredProducts = this.products);
      } else {
        this.filteredProducts = this.products.filter((product) => {
          return product.category === this.chosenCategory;
        });
      }

      //console.log(this.filteredProducts);
      this.showCategorizedProducts = true;
      return this.filteredProducts;
    },
    toggleDisplayMode() {
      this.displayMode = this.displayMode === "grid4" ? "grid2" : "grid4";
    },

    toggleCartVisibility() {
      this.showCart = !this.showCart;
    },
    //you can place any name could be x, because the reference od x we have given it on the button
    addToCart(anyNameid) {
      this.cartItem = this.products.find((product) => product.id == anyNameid);
      //buscar el id i el prodcute i llavors fer un push del producte trobat al cart
      //mes un contador q et suma els productes
      //si dona temps mostrar la quantiat el nom del prducte i el preu
      //dspres una soma del total
      //el parametre id es el product.id que li he passat quan he fet click.
      if (this.cartItem) {
        //this.productsCart.push(cartItem);
        console.log(this.cartItem);
        this.$emit("sendProductToBuy", this.cartItem);
      }
    },
    /*
  getDesiredProduct(product) {
    console.log(this.product);
    this.$emit("sendProductToBuy", product);
  },*/
  },
};
</script>

<style>
.read-the-docs {
  color: #888;
}

#display {
  border-color: #900404;

  padding: 3px;
}
</style>
