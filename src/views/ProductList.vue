<!--//Criteria3 -  "Review the code in ProductList.vue and fix the bugs that exist." -->
<template>
  <div id="filtering">
    <label for="selector">
      Filter:
      <!--//Criteria4 & Criteria7 - Additional filters and options in ProductList.vue-->
      <select v-model="select" id="selector">
        <option value="all" selected>All</option>
        <option value="purchased">Purchased</option>
        <option value="unpurchased">Unpurchased</option>
        <option value="onetime">One-Time Purchases</option>
        <option value="subscriptions">Subscriptions</option>
      </select>
    </label>

    <h1>SELECTED FILTER: {{ selectedFilter }}</h1>
    <section class="card-grid">
      <!--//Criteria2 - "Use your component in ProductList.vue."-->
      <Product
        class="card"
        v-for="(product, idx) in sortedProducts"
        :key="idx"
        :product="product"
      />
    </section>
  </div>
</template>

<script>
import Product from "../components/Product";
const productItems = require("@/assets/products.json");

export default {
  name: "ProductList",
  components: {
    Product
  },
  computed: {
    products() {
      if (this.selectedFilter == "all") {
        let products = [...productItems];
        return products;
      } else if (this.selectedFilter == "purchased") {
        let products = [...productItems];
        //Filtering the duplicated array for only [purchased: true] results
        let purchased = products.filter(function(product) {
          return product.purchased == true;
        }); //console.log(purchased); Test

        products = purchased; // overwritting th array
        return products;
      } else if (this.selectedFilter == "unpurchased") {
        let products = [...productItems];

        let unpurchased = products.filter(function(product) {
          return product.purchased == false;
        });

        products = unpurchased;
        return products;
      } else if (this.selectedFilter == "onetime") {
        let products = [...productItems];
        let onetime = products.filter(function(product) {
          return product.type == "onetime";
        });

        products = onetime;
        return products;
      } else if (this.selectedFilter == "subscriptions") {
        let products = [...productItems];
        let subs = products.filter(function(product) {
          return product.type == "recurring";
        });

        products = subs;
        return products;
      }
      return "Product";
    },
    //Criteria9 - Correct order - "The products should be displayed in the correct order"
    sortedProducts: function() {
      function order(a, b) {
        if (a.order < b.order) return -1;
        if (a.order > b.order) return 1;
        return 0;
      }
      // return this.users.sort(order); // sorts in-place
      return [...this.products].sort(order); // shallow clone + sort
    }
  },
  data() {
    //Default option
    return {
      select: "all",
      selectedFilter: "all"
    };
  },
  watch: {
    select: function(oldVal) {
      this.selectedFilter = oldVal;
    }
  }
};
</script>

<style lang="scss">
//Criteria5 - Responsive columns & media queries
.card-grid {
  display: grid;
  justify-items: center;
  align-items: center;
  grid-template-columns: repeat(4, minmax(290px, 1fr)); /* see notes below */
  grid-auto-rows: minmax(200px, auto);
  grid-gap: 1rem;
  margin: 20px;
  .card {
    border-radius: 8px;
    position: relative;
    overflow: hidden;
    -webkit-box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12),
      0 1px 2px rgba(0, 0, 0, 0.24);
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
    transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
    display: flex;
    cursor: pointer;
    -ms-flex-direction: column;
    flex-direction: column;
    &:hover {
      box-shadow: 0 14px 28px #42b983, 0 10px 10px rgba(0, 0, 0, 0.22);
    }
  }
}
// Queries
@media screen and (max-width: 600px) {
  // <600px
  .card-grid {
    grid-template-columns: repeat(1, minmax(320px, 1fr));
  }
}
@media (min-width: 601px) and (max-width: 800px) {
  // <601-800px>
  .card-grid {
    grid-template-columns: repeat(2, minmax(150px, 1fr));
  }
}
@media (min-width: 801px) and (max-width: 1024px) {
  // <801-1024px>
  .card-grid {
    grid-template-columns: repeat(3, minmax(200px, 1fr));
  }
}
@media screen and (min-width: 1025px) {
  // >1025px
  .card-grid {
    grid-template-columns: repeat(4, minmax(200px, 1fr));
  }
}
</style>
