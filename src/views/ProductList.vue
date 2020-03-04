<template>
  <div class="product-list">
    <label for="selector">
      Filter:
      <select v-model="select" id="selector">
        <option value="all" selected>All</option>
        <option value="purchased" selected>Purchased</option>
        <option value="unpurchased" selected>Unpurchased</option>
        <option value="onetime" selected>One time purchases</option>
        <option value="recurring" selected>Subscriptions</option>
      </select>
    </label>
    <h1>SELECTED FILTER: {{ selectedFilter }}</h1>
    <div class="products">
      <Product
        v-for="(product, index) in products"
        v-bind:product="product"
        v-bind:key="product.title + index"
      />
    </div>
  </div>
</template>

<script>
const productItems = require("@/assets/products.json");
import Product from "../components/Product.vue";

export default {
  name: "ProductList",
  components: {
    Product
  },
  computed: {
    products() {
      let products;
      switch (this.selectedFilter) {
        case "purchased":
          products = productItems.filter(product => product.purchased);
          break;
        case "unpurchased":
          products = productItems.filter(product => !product.purchased);
          break;
        case "onetime":
          products = productItems.filter(product => product.type === "onetime");
          break;
        case "recurring":
          products = productItems.filter(
            product => product.type === "recurring"
          );
          break;
        case "all":
        default:
          products = productItems;
          break;
      }
      return products.sort((a, b) => a.order - b.order);
    }
  },
  data() {
    return {
      select: "all",
      selectedFilter: "all"
    };
  },
  watch: {
    // eslint-disable-next-line no-unused-vars
    select: function(newVal, oldVal) {
      this.selectedFilter = newVal;
    }
  }
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

.product-list {
  max-width: 1600px;
  margin: 0 auto;
}

.products {
  // display: flex;
  // flex-wrap: wrap;
  // justify-content: space-around;
  // align-items: flex-start;

  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
}
</style>
