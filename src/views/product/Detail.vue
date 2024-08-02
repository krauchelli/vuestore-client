<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div>
        <div id="page-wrap" v-if="product"> <!-- menampilkan data product jika ada dengan cara v-if dan v-else -->
          <h4 v-if="notif" class="notif">Item added successfully</h4>
          <div id="img-wrap">
            <img :src="`http://localhost:8000${product[0].imageUrl}`" alt="">
          </div>
          <div id="product-details">
            <h1>{{ product[0].name }}</h1>
            <h3 id="price">Rp{{ product[0].price }}</h3>
            <p>Average Rating: {{ product[0].averageRating }}</p>
            <button id="add-to-cart" @click="addToCart(product[0].code)" >Add to Cart</button>
            <p>{{ product[0].description }}</p>
          </div>
        </div>

        <NotFound v-else />
    </div>
</template>

<script>
import axios from 'axios';
//import { products } from '../../data-seed'
import NotFound from '../errors/NotFound.vue'

export default {
  components:
  {
    NotFound
  },
  data() {
    return {
      product: [],
      notif: false
    }
  },
  // method untuk menambahkan barang ke cart
  methods: {
    async addToCart(product) {
      console.log(product);
      await axios.post('http://localhost:8000/api/orders/user/1/add-to-cart', {
        productCode: product
      });
      this.notif = true;
    }
  },
  async created() {
    const code = this.$route.params.id; // mengambil id barang dari route
    const result = await axios.get(`http://localhost:8000/api/products/${code}`); // mengambil data barang berdasarkan id
    this.product = result.data;
  },
  // menggunakan compute untuk mengambil data spesifik dari products
  /*computed: {
    product() {
      return this.products.find(p => {
        return p.id === this.$route.params.id;
      })
    }
  },*/
}
</script>

<style scoped>
  #page-wrap {
    margin-top: 16px;
    padding: 16px;
    max-width: 600px;
  }

  #img-wrap {
    text-align: center;
  }

  img {
    width: 400px;
  }

  #product-details {
    padding: 16px;
    position: relative;
  }

  #add-to-cart {
    width: 100%;
  }

  #price {
    position: absolute;
    top: 24px;
    right: 16px;
  }

  .notif {
    background-color: #41B883;
    color: white;
    padding: 3%;
    border-radius: 8px;
    text-align: center;
  }
</style>