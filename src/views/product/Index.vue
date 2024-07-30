<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <div id="page-wrap">
        <div class="grid-wrap">
            <ProductItem 
              v-for="product in products"
              :key="product.id" 

              :productProp="product"
            /> <!-- menampilkan product item, menggunakan konsep component dan prop
              'product' pada :produt adalah prop yang nanti akan di passing ke ProductItem.vue,
              sedangkan nilai dari product adalah product yang di loop dari 'products' -->
            -->
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import ProductItem from '../../components/ProductItem.vue'

export default {
    components: {
        ProductItem
    },
    data() {
        return {
            products: []
        }
    },
    async created() {
        const result = await axios.get('http://localhost:8000/api/products');
        this.products = result.data;
    }
}
</script>

<style scoped>
  .grid-wrap {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    margin-top: 16px;
  } 
</style>