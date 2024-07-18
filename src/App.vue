<template>
  <div id="app">
    <nav>
      <router-link to="/">Product</router-link> |
      <router-link :to="{ name: 'product-detail', params: {id: 123}}">Detail</router-link> | 
      <router-link to="/cart">Cart</router-link> |
    </nav>
    <router-view/>
  </div>
</template>

<style>

</style>
