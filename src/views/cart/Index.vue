<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <div id="page-wrap">
      <h1>Shopping Cart</h1>
      <ItemCart 
        v-for="item in cartItems"
        :key="item.id"
        :item="item"
        v-on:remove-item="removeFromCart($event)"
      /> <!-- $event akan menangkap nilai dari child component (ItemCart.vue) dengan variabel $emit, parameter kedua sebagai argumen nya, yaitu item.code -->
      <h3 id="total-price">Total: Rp{{ totalPrice }}</h3>
      <button id="checkout-button">Checkout</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
//import { cartItems } from '../../data-seed';
import ItemCart from '../../components/ItemCart.vue';

export default {
  components: {
    ItemCart
  },
  data() {
    return {
      cartItems: []
    }
  },
  methods: {
    async removeFromCart(code) {
      await axios.delete(`http://localhost:8000/api/orders/user/1/remove-from-cart/${code}`);
      this.cartItems = this.cartItems.filter(item => item.code !== code); // menghapus item dari cartItems berdasarkan code setelah proses delete
    }
  },
  computed: {
    totalPrice() {
      return this.cartItems.reduce((sum, item) => {
        return sum + Number(item.price);
      }, 0);
    }
  },
  async created() {
    const result = await axios.get('http://localhost:8000/api/orders/user/1');
    // logika untuk mengambil data cart_items dari result.data
    // cara kerja Object.assign adalah menggabungkan semua object yang ada di dalam array menjadi satu object dari method map yang dijalankan
    // kemudian hasil dari Object.assign akan di assign ke dalam data cartItems
    let data = Object.assign({},
      ...(result.data.map(
        item => ({
          cart_items: item.products
        })
      ))
    );
    this.cartItems = data.cart_items;
    console.log(`hasil dari cart: ${this.cartItems}`);
  }
}
</script>

<style scoped>
    h1 {
    border-bottom: 1px solid #41B883;
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
</style>