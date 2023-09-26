<template>
  <div>
    <!-- <h1>this pretends to be a Cart</h1> -->
    <!-- Your Cart component content -->
    <ul>
      <li v-for="(product, index) in cartItems" :key="index">
        {{ product.name }} - {{ product.price }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Cart",
  components: {
    productsToAddInCart: Array,
  },
  data() {
    return {
      cart: [],
      showCart: false,
    };
  },
};
</script>

<style></style>
