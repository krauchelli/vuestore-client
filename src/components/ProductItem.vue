<!-- eslint-disable vue/no-multiple-template-root -->
<template>
    <div class="product-item">
        <img :src="`http://localhost:8000${productProp.imageUrl}`" alt="">
        <h3 class="product-name">{{ productProp.name }}</h3>
        <p class="product-price">Rp{{ productProp.price }}</p>
        <router-link :to="{ name: 'product-detail', params: {id: productProp.code}}">
            <button>Detail</button>
        </router-link> | 
    </div>
</template>

<script>
export default {
    props: [
        'productProp'
    ]
}
</script>

<style scoped>
.product-item {
    align-items: center;
    border-radius: 8px;
    box-shadow: 0px 2px 5px #888;
    display: flex;
    flex-direction: column;
    margin-bottom: 2%;
    padding: 20px;
    position: relative;
    width: 32%;
  }

  .product-name {
    margin-bottom: 0;
  }

  img {
    height: 200px;
    width: 200px;
    border-radius: 5%;
  }

  a {
    width: 100%;
  }

  button {
    width: 100%;
  }
</style>