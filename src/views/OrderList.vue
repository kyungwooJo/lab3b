<template>
<div class="wrapper">
  <div class="products">
    <p v-if=" this.$root.$data.isEmpty">There is no item in your cart</p>
    <p v-else>Here is your Order list!</p>
    <div class="product" v-for="product in this.$root.$data.cart" :key="product.id">
      <div class="info">
        <h1>{{product.productName}}</h1>
        <p>Price: {{product.productPrice}}</p>
        <p>TotalQty: {{product.totalQty}}</p>
      </div>
      <div class="image">
        <img :src= "'/images/products/' + product.productImageUrl">
      </div>
      <div class="price">
        <h2>{{product.price}}</h2>
        <button @click="removeFromCart(product.productId)" class="auto">Remove</button>
      </div>
    </div>
  </div>
</div>
</template>


<script>
export default {
  
  name: 'orderList',  
  methods: {


      removeFromCart(id) { 

      this.$root.$data.totalOrderListNum = this.$root.$data.totalOrderListNum - this.$root.$data.cart.filter(obj => {return obj.productId === id})[0].totalQty ;
     
      if(this.$root.$data.totalOrderListNum == 0){
          this.$root.$data.isEmpty = true;
      }

      this.$root.$data.cart = this.$root.$data.cart.filter(obj => {
         return obj.productId !== id;
        }); 
    }
  }
  
}
</script>