<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div>
        <div id="page-wrap" v-if="product"> <!-- menampilkan data product jika ada dengan cara v-if dan v-else -->
          <div id="img-wrap">
            <img :src="product.imageUrl" alt="">
          </div>
          <div id="product-details">
            <h1>{{ product.name }}</h1>
            <h3 id="price">Rp{{ product.price }}</h3>
            <p>Average Rating: {{ product.averageRating }}</p>
            <button id="add-to-cart">Add to Cart</button>
            <p>{{ product.description }}</p>
          </div>
        </div>

        <NotFound v-else />
    </div>
</template>

<script>
import { products } from '../../data-seed'
import NotFound from '../errors/NotFound.vue'

export default {
  components:
  {
    NotFound
  },
  data() {
    return {
      products
    }
  },
  // menggunakan compute untuk mengambil data spesifik dari products
  computed: {
    product() {
      return this.products.find(p => {
        return p.id === this.$route.params.id;
      })
    }
  },
  mounted() {
    console.log(this.product);
  }
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

</style>