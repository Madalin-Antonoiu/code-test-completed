
<!-- Acceptance Criteria Nr.3 -  "Review the code in ProductList.vue and fix the bugs that exist." -->
<template>
  <div>

    <label for="selector">
      Filter:
      <!-- Criteria.7 - Extra filtering options  -->
      <select v-model="select" id="selector">
        <option value="all" selected>All</option>
        <option value="purchased">Purchased</option>
        <option value="unpurchased">Unpurchased</option>
        <option value="onetime">One time purchases</option>
        <option value="subscriptions">Subscriptions</option>
      </select>
    </label>

    <h1>SELECTED FILTER: {{ selectedFilter }}</h1>

    <section class="cards">
       <!--Product.vue -->
      <Product class="card" v-for="(product, idx) in sortedProducts" :key="idx" :product="product" />
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
        //console.log(products[0]);
        //products.sort(dynamicSort("order")); TBD
        return products;

      } else if (this.selectedFilter == "purchased") {
        let products = [...productItems];

        //Filtering the duplicated array for only [purchased: true] results
        let purchased = products.filter(function(product){
          return product.purchased == true;
        });//console.log(purchased); Test, works!
        
        products = purchased; // overwritting th array
        return products;

      } else if (this.selectedFilter == "unpurchased"){
        let products = [...productItems];

        let unpurchased = products.filter(function(product){
          return product.purchased == false;
        });

        products = unpurchased; 
        return products;
      } else if (this.selectedFilter == "onetime"){
        let products = [...productItems];
        let onetime = products.filter(function(product){
          return product.type == "onetime";
        });

        products = onetime; 
        return products;
      } else if (this.selectedFilter == "subscriptions"){
        let products = [...productItems];
        let subs = products.filter(function(product){
          return product.type == "recurring";
        });

        products = subs; 
        return products;
      };

      return "Product";
    },
    // Acceptance Criteria Nr.9: "The products should be displayed in the correct order" 
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
      selectedFilter: "all",
      

    };
  },
  watch: {
    select: function(oldVal) {// fix
      this.selectedFilter = oldVal;
    }
  }
  
};
</script>

<style lang="scss">


/***************************           Cards            *******************************/

.cards {
  display: grid;
  justify-items: center;
  align-items: center;
  grid-template-columns: repeat(4, minmax(290px, 1fr)); /* see notes below */
  grid-auto-rows: minmax(200px, auto);
  grid-gap: 1rem;
  margin: 20px;
}

.card {
  /*height: 200px;*/
  /*background: red;*/
  -webkit-box-shadow: 0 2px 2px rgba(0, 0, 0, 0.15);
  box-shadow: 0 2px 2px rgba(0, 0, 0, 0.15);
  display: flex;
  /* -webkit-box-orient: vertical; */
  /* -webkit-box-direction: normal; */
  -ms-flex-direction: column;
  flex-direction: column;
  position: relative;
  

} 



// Acceptance Criteria Nr.5 - Responsive columns and media queries 
@media screen and (max-width: 600px) { // <600px
  .cards {
    grid-template-columns: repeat(1, minmax(320px, 1fr));
 
  }
}

@media (min-width: 601px) and (max-width: 800px) { // <601-800px>
  .cards {
    grid-template-columns: repeat(2, minmax(150px, 1fr));
 
  }
}

@media (min-width: 801px) and (max-width: 1024px) { // <801-1024px>
  .cards {
grid-template-columns: repeat(3, minmax(200px, 1fr));
  }
}

@media screen and (min-width: 1025px) { // >1025px
  .cards {
     grid-template-columns: repeat(4, minmax(200px, 1fr));
  }
}

</style>