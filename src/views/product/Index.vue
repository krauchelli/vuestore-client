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
import { products } from '../../data-seed' 
import ProductItem from '../../components/ProductItem.vue'

export default {
    components: {
        ProductItem
    },
    data() {
        return {
            products
        }
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