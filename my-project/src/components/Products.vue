<template>
  <div class="mx-12">
    <button type="button" @click="getProducts">show products</button>
  </div>
  <div class="grid grid-cols-3 gap-4">
    <div
      v-for="(product, index) in products"
      :key="id"
      class="h-112 p-10 relative group"
    >
      <img
        :src="product.image"
        :alt="product.category"
        class="h-112 p-10 group-hover:hidden"
      />
      <div class="absolute inset-0 p-10 hidden group-hover:block">
        <h4 class="text-xl font-bold">{{ product.title }}</h4>
        <p class="mt-2">{{ product.description }}</p>
        <p class="mt-2 font-bold">Price: ${{ product.price }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Products",
  props: [""],
  data() {
    return {
      products: "",
    };
  },
  methods: {
    async getProducts() {
      //const randomNumber = Math.floor(Math.random() * 20) + 1;
      //const response = await fetch(`https://fakestoreapi.com/${randomNumber}`);
      const response = await fetch("https://fakestoreapi.com/products");
      const data = await response.json();
      this.products = data;
    },
  },
  //   mounted: {
  //     async getProducts() {
  //       //const randomNumber = Math.floor(Math.random() * 20) + 1;
  //       //const response = await fetch(`https://fakestoreapi.com/${randomNumber}`);
  //       const response = await fetch("https://fakestoreapi.com/products");
  //       const data = await response.json();
  //       this.products = data;
  //     },
  //  },
};
</script>

<style>
.read-the-docs {
  color: #888;
}
</style>
