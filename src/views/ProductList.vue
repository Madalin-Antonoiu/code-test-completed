<template>
  <div>
    <label for="selector">
      Filter:
      <select v-model="select" id="selector">
        <option value="all" selected>All</option>
        <option value="purchased">Purchased</option>
        <option value="unpurchased">Unpurchased</option>
        <option value="onetime">One time purchases</option>
        <option value="subscriptions">Subscriptions</option>
      </select>
    </label>

    <h1>SELECTED FILTER: {{ selectedFilter }}</h1>
    <!-- This is the main list view -->

  <div class="row">
    <aside class="aspect-ratio"></aside>

    <div class="column" v-for="(product, idx) in products" :key="idx">

          <div class="card">
            <img class="img" :src="`${product.image}`" :alt="`${product.description}`">
            <div class="footer">
              <h3>{{ product ? product.title : "" }}</h3>
              <p>{{ product ? product.price : "" }}</p>
              <p>{{ product ? product.description : "" }}</p>
              <div class="avatar">
                <span class="active-state"></span>
                <span class="oval"></span>
              </div>
            </div>

            </div>
          </div>
  
      </div>
  
  </div>
</template>

<script>
//import Product from "../components/Product";
const productItems = require("@/assets/products.json");



export default {
  name: "ProductList",
  components: {
    //Product
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
    select: function(oldVal) {//2nd fix
      this.selectedFilter = oldVal;
    }
  }
  
};
</script>

<style lang="scss">

:root {
	/* variables */
	--spacing: 24px;
	--min-card-width: 250px;
	--ratio-percent: 75%; /* Perfect 4:3 Ratio*/
	--addl-height: 100px;
}

* {
  box-sizing: border-box;
}



body {
  font-family: Arial, Helvetica, sans-serif;
}

/* Float four columns side by side */
.column {
  float: left;
  width: 25%;
  padding: 10px;
}

.img{
    height: auto;
    width: 100%;
    vertical-align: middle;
    border-radius: 8px 8px 0px 0px ;
   

}
/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}

/* Responsive columns - Criteria 1 */
@media screen and (max-width: 600px) { // <600px
  .column {
    width: 100%;
    display: block;
    margin-bottom: 20px;
  }
}

@media (min-width: 601px) and (max-width: 800px) { // <601-800px>
  .column {
    width: 50%;
    display: block;
    margin-bottom: 20px;
  }
}

@media (min-width: 801px) and (max-width: 1024px) { // <801-1024px>
  .column {
    width: 33.3%;
    display: block;
    margin-bottom: 20px;
  }
}

@media screen and (min-width: 1025px) { // >1025px
  .column {
    width: 25%;
  }
}

/* Style the counter cards */
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  text-align: center;
  color: #f1f1f1;
  border-radius:  0px 0px 8px 8px;
  position: relative; // for .avatar's absolute positioning
}

.footer{
  padding: 16px;
  background: #282828;
}

.avatar{
  position: absolute;
  width: 32px;
  height: 32px;
  left: 85%;
  top: 72.5%;
  background: url(../assets/avatar.png);
  background-size:cover;
  border-radius: 50%;
    .active-state{
      position: absolute;
      //visibility: hidden;
      left: 75%;
      right: 0%;
      top: 0%;
      bottom: 75%;
      background: #7ED321;
      border-radius:50%;
    }
  }



</style>