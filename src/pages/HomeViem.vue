<script>
export default {
    methods: {
        goToAbout() {
            this.$router.push('/about')
        },
    },
}
</script>

<template>
    <div>
      <h1>Home Page</h1>
      <p>Selamat Datang DiToko Buah Ellsya</p>
      <CarouselAndCard />
    </div>
  </template>
  
  <script setup>
  import CarouselAndCard from '../components/CarouselAndCard.vue'
  </script>