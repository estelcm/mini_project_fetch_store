<template>
  <div class="mt-30">
    <!-- Dropdown to select a category -->
    <label for="text">Categories: </label>
    <!-- aquest de sota el comento perque es en cas de ue la categoria seleccionada l'enviem a App i de app la tornem a enviar a Products -->
    <!-- <select v-model="selectedCategory" @change="sendCategory"> -->

    <select v-model="selectedCategory" @change="sendCategory">
      <option value="all Categories">All Categories</option>
      <option value="jewelery">Jewelery</option>
      <option value="electronics">Electronics</option>
      <option value="men's clothing">Men's Clothing</option>
      <option value="women's clothing">Women's Clothing</option>
    </select>
  </div>
</template>

<script>
export default {
  name: "CategoryFilter",
  props: {},
  data() {
    return {
      selectedCategory: "all Categories",
    };
  },
  computed: {},
  methods: {
    sendCategory() {
      this.$emit("chosenCategory", this.selectedCategory);
    },
  },
};
</script>

<style></style>
