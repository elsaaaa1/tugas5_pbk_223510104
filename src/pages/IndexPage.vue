<template>
    <q-page>
      <Carousel />
      <ProductList />
    </q-page>
  </template>
  
  <script>
  import Carousel from '../components/Carousel.vue';
  import ProductList from '../components/ProductList.vue';
  
  export default {
    name: 'IndexPage',
    components: {
      Carousel,
      ProductList
    }
  };
  </script>
  