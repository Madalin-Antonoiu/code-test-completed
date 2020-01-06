<template>
  <!--//Criteria1 - Product.vue "Create a component for displaying a product in a list. Product.vue"-->
  <div class="product">
    <img :src="`${product.image}`" :alt="`${product.description}`" />
    <div class="card-content">
      <!-- Bonus: Dinamically created badge (if only discounted) for enhanced discount effect? Checked!-->
      <span v-bind:class="{ promotionActive: product.discount }">
        {{ product.discount ? "-" + product.discount : "" }}</span
      >
      <p>{{ product ? product.title : "" }}</p>
      <!--Bonus: Casually striking-through the old price with a line IF only there is a discount associated? Why not?-->
      <p>
        <span
          v-bind:class="{ lineThrough: product.discount }"
          class="full-price"
          >{{ product ? product.price : "" }}</span
        >
        <!--//Criteria8 - The logic [in one line]: If discount exist, substract from the full price the multiplication between full price and discount divided by 100.0-->
        <span class="discount">{{
          product.discount
            ? product.price -
              (product.price * parseInt(product.discount)) / 100.0
            : ""
        }}</span>
      </p>
      <p class="description">{{ product ? product.description : "" }}</p>
      <div class="avatar">
        <!-- Bonus: Added active state based on the same JSON file. Green is the new gray. -->
        <span
          class="activeState"
          v-bind:class="{ isActive: product.active }"
        ></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Product",
  props: {
    product: {
      type: Object,
      required: true
    }
  }
};
</script>

<style lang="scss">
//Criteria10 - Following Figma's design as close as possible.
@font-face {
  font-family: "Gilroy";
  src: url("/assets/fonts/MyFontSerifReg.otf");
}
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
a {
  text-decoration: none;
  color: orange;
}
p {
  margin-left: 16px;
  margin-bottom: 8px;
  margin-top: 0px;
}
img {
  display: block;
  border: 0;
  width: 100%;
  height: 180px;
  border-radius: 8px 8px 0px 0px;
}
.discount {
  color: #f03013;
  padding-left: 3px;
}
.promotionActive {
  position: absolute;
  left: 2%;
  bottom: 31%;
  background: #ff4200;
  width: 60px;
  height: 18px;
  text-align: center;
  vertical-align: middle;
}
.lineThrough {
  text-decoration: line-through;
  text-decoration-color: rgb(0, 0, 0);
  opacity: 0.3;
}
.card-content {
  color: #ffffff;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-flex: 1;
  -ms-flex: 1;
  flex: 1;
  background: #282828;
  border-radius: 0px 0px 8px 8px;
  font-family: "Gilroy";
  font-style: normal;
  font-weight: 600;
  font-size: 16px;
  line-height: 19px;
  text-align: left;
  padding-top: 16px;
  .description {
    font-family: "Gilroy";
    font-style: normal;
    font-weight: 500;
    font-size: 12px;
    line-height: 14px;
    color: #bdbdbd;
  }
}
.panel.card-panel .panel-header {
  font-size: 0.75rem;
  font-weight: 400;
}
.panel.card-panel .panel-content {
  -webkit-box-flex: 1;
  -ms-flex: 1;
  flex: 1;
}
footer {
  min-height: 30px;
  font-size: 0.5rem;
  background: #282828;
}
.category {
  position: absolute;
  top: 110px;
  left: 0;
  color: #fff;
  background: #e74c3c;
  padding: 10px 15px;
  font-size: 14px;
  font-weight: 600;
  text-transform: uppercase;
}
.avatar {
  position: absolute;
  width: 32px;
  height: 32px;
  right: 5%;
  top: 72.5%;
  background: url(../assets/avatar.png);
  background-size: cover;
  border-radius: 50%;
  .activeState {
    position: absolute;
    //visibility: hidden; //Grey/Green elipse display toggle
    left: 75%;
    right: 0%;
    top: 0%;
    bottom: 75%;
    background: grey;
    border-radius: 50%;
  }
  .isActive {
    position: absolute;
    left: 75%;
    right: 0%;
    top: 0%;
    bottom: 75%;
    border-radius: 50%;
    background: #7ed321 !important;
  }
}
</style>
