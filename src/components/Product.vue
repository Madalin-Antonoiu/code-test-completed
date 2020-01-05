<template>

  <div class="product">
      <div class="header"><!-- DO JS dynamic insertion for every pic here--></div>
      <div class="footer">
        <div class="title">Yearly Membership</div>
        <div class="price">120000</div>
        <div class="description">Yearly membership to MyPTHub</div>
        <div class="avatar">
          <span class="active-state"><span class="oval"></span></span>
        </div>
      </div>
  </div>
  
</template>

<script>

export default {
  name: "Product"
};
</script>

<style lang="scss">
$width: 465px;
$height: 350px;
$radius: 8px;

.product {
  max-width: $width;
  max-height: $height;
  background: #282828;
  opacity: 0.8;
  border-radius: $radius;
  position: relative;
  .header{
   background: url(https://picsum.photos/id/0/400/300); //swap for img {{ from JSON}}
   background-repeat: no-repeat;
   background-size: cover;
   height: 250px;
   width: inherit;
  border-radius: $radius;
  }

  .footer{
    width: $width;
    height: 100px;
    .title, & .price{
      //position: absolute;
      margin: 16px;
      font-family: Gilroy;
      font-style: normal;
      font-weight: 600;
      font-size: 16px;
      line-height: 19px;
      /* identical to box height, or 119% */
      display: flex;
      align-items: center;
      /* White */
      color: #FFFFFF;
      }

      .description{
        position: absolute;
        left: 16px;
        /* Minion */
        font-family: Gilroy;
        font-style: normal;
        font-weight: 500;
        font-size: 12px;
        line-height: 14px;
        /* identical to box height, or 117% */
        display: flex;
        align-items: center;
        /* GreyOne */
        color: #BDBDBD;
        border-radius: 8px;
        }

        .avatar{
          position: absolute;
          width: 32px;
          height: 32px;
          left: 80%;
          top: 75%;
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
  }
}
</style>
