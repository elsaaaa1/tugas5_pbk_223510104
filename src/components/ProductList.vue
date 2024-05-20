<template>
    <div class="q-pa-md">
      <div class="row q-col-gutter-md justify-center">
        <ProductCard
          v-for="product in products"
          :key="product.id"
          :image="product.image"
          :title="product.title"
          :description="product.description"
        />
      </div>
    </div>
  </template>
  
  <script>
  import ProductCard from './ProductCard.vue';
  
  export default {
    name: 'ProductList',
    components: {
      ProductCard
    },
    data() {
      return {
        products: [
          { id: 1, image: 'https://via.placeholder.com/200', title: 'Product 1', description: 'Description of Product 1' },
          { id: 2, image: 'https://via.placeholder.com/200', title: 'Product 2', description: 'Description of Product 2' },
          { id: 3, image: 'https://via.placeholder.com/200', title: 'Product 3', description: 'Description of Product 3' }
        ]
      };
    }
  };
  </script>
  