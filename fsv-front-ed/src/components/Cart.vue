<template>
    <div>
        <h1>Shopping Cart</h1>
        <div v-if="products.length > 0">
            <CartItem 
                v-for="product in products"
                @remove-from-cart="$emit('remove-from-cart', $event)"
                :key="product.id"
                class="product-container"
                :product="product" />
            <h3 id="total-price">Total: ${{totalPrice}}</h3>
            <button id="checkout-button">Proceed to Checkout</button>
        </div>
        <div v-else>
            <p>You haven't added anything to your shopping cart.</p>
        </div>
    </div>    
</template>

<script>
import CartItem from './CartItem.vue';

export default {
    name: 'Cart',
    props: ['products'],
    components: {
        CartItem,
    },
    computed: {
      totalPrice() {
        return this.products.reduce(
          (sum, item) => sum + Number(item.price),
          0,
        );
      }
    }    
}
</script>