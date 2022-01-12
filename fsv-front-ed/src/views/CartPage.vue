<template>
  <div id="page-wrap">
    <Cart 
      class="details-wrap" :products="cartItems"
      @remove-from-cart="removeFromCart($event)" 
    />
  </div>
</template>

<script>
import axios from 'axios';
//import {cartItems} from '../fake-data';
import Cart from '../components/Cart.vue';

export default {
    name: 'CartPage',
    components: {
      Cart,
    },
    data() {
      return{
        //cartItems,
        cartItems: [],
      }
    },
    async created(){
      const result = await axios.get('/api/users/12345/cart');
      const cartItems = result.data;
      this.cartItems = cartItems;
    },
    methods: {
      async removeFromCart(productId){
        const result = await axios.delete(`/api/users/12345/cart/${productId}`);
        this.cartItems = result.data;
      }
    }
}
</script>

<style scoped>
  h1 {
    border-bottom: 1px solid black;
    margin: 0;
    margin-top: 16px;
    padding: 16px;
  }

  #total-price {
    padding: 16px;
    text-align: right;
  }

  #checkout-button {
    width: 100%;
  }

  .product-container {
    align-content: 'center';
    border-bottom: 1px solid #ddd;
    display: flex;
    padding: 16px;
    width: 100%;
  }

  .product-image {
    flex: 1;
    height: 100px;
    max-width: 100px;
  }

  .details-wrap {
    padding: 0 16px;
    flex: 3;
  }

  .remove-button {
    flex: 1;
    margin: auto;
  }
</style>
