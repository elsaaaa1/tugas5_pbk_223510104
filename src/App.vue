<template>
  <q-layout view="hHh lpR fFf">
    <!-- Navbar -->
    <q-header elevated class="bg-primary text-white" height-hint="98">
      <q-toolbar>
        <q-btn flat round dense icon="menu" aria-label="Menu" @click="drawer = !drawer" />
        <q-toolbar-title>
          <q-avatar>
            <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
          </q-avatar>
          Fruit Shop Ellsya
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <!-- Drawer Menu -->
    <q-drawer v-model="drawer" side="left" overlay>
      <q-list>
        <q-item clickable v-ripple>
          <q-item-section>Home</q-item-section>
        </q-item>
        <q-item clickable v-ripple>
          <q-item-section>Fruits</q-item-section>
        </q-item>
        <q-item clickable v-ripple>
          <q-item-section>Contact</q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <!-- Page Content -->
    <q-page-container>
      <router-view />
      <div class="q-pa-md">
        <!-- Carousel -->
        <q-carousel
          v-model="slide"
          animated
          control-color="white"
          arrow-color="white"
          height="300px hd"
          class="rounded-borders"
          infinite
          autoplay
        >
          <q-carousel-slide v-for="(image, index) in carouselImages" :key="index" :name="index" :img-src="image.src">
            <div class="absolute-bottom text-subtitle1 text-center text-shadow">
              {{ image.caption }}
            </div>
          </q-carousel-slide>
        </q-carousel>

        <!-- Cards -->
        <div class="q-gutter-md q-mt-md row">
          <q-card 
            v-for="(product, index) in products" 
            :key="index" 
            class="col-xs-12 col-sm-6 col-md-4 card-hover"
          >
            <q-card-section>
              <q-img :src="product.image" :alt="product.name" class="card-img"></q-img>
              <div class="text-h6">{{ product.name }}</div>
              <div>{{ product.description }}</div>
              <div class="text-subtitle1 text-bold">${{ product.price }}</div>
            </q-card-section>
            <q-card-actions align="right">
              <q-btn flat label="Details" @click="showDetails(product)" />
            </q-card-actions>
          </q-card>
        </div>
      </div>
    </q-page-container>

    <!-- Footer -->
    <q-footer elevated class="bg-grey-8 text-white">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
          </q-avatar>
          <div>Fruit Shop Ellsya</div>
        </q-toolbar-title>
        <q-btn flat round dense icon="facebook" color="white" aria-label="Facebook" />
        <q-btn flat round dense icon="twitter" color="white" aria-label="Twitter" />
        <q-btn flat round dense icon="instagram" color="white" aria-label="Instagram" />
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
export default {
  data() {
    return {
      drawer: false,
      slide: 0,
      carouselImages: [
        { src: 'data:image/jpeg;base64,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' },
        { src: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTOgM9-7fXpn9MnN6p5vv_1MZMSW33eYs3Mjw&s' },
    ],

      products : [
        {
          name: 'Apple',
          description: 'Fresh and juicy apples.',
          price: 1.2,
          image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ8FhhR5la9xfUxucuz8_ED6ErODQ9Dzh18kA&s'
        },
        {
          name: 'Banana',
          description: 'Sweet and ripe bananas.',
          price: 0.8,
          image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRiqKxU5pFyzhrt-SoQeNV8wAnrShtp9CwfAg&s'
        },
        {
          name: 'Peach',
          description: 'Soft and Delicious.',
          price: 2.3,
          image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRJ_QzJWQAwLllv21AB7i03d0rjBzijYJ0LFA&s'
        },
        {
          name: 'Mango',
          description: 'Delicious.',
          price: 1.9,
          image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSgdxIM8-NGWkD9JMjL2ESy6OjflwiE-Q3ASA&s'
        },
        {
          name: 'Kiwi',
          description: 'Fresh and sweet.',
          price: 1.7,
          image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR4ogtUI1FELFMuVPwvFIYfrVM1toHKSD_9Vw&s'
        },
        {
          name: 'Strawberry',
          description: 'Delicious and fresh strawberries.',
          price: 2.5,
          image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRIFweBcZpWcicser-eaWu_Yb1WP6PuponT7g&s'
        }
      ]
    }
  
  },
  methods: {
    showDetails(product) {
      alert(`Details for ${product.name}`)
    },
    alertInfo(img) {
      alert(`Image: ${img}`);
    }
  }
}
</script>

<style>
.card-img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 8px;
}

.card-hover {
  transition: transform 0.3s, box-shadow 0.3s;
  border-radius: 8px;
}

.card-hover:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 16px rgba(236, 78, 155, 0.2);
}

.carousel-image {
  width: 100%;
  height: 300px;
  object-fit: cover;
}

.carousel-caption {
  position: absolute;
  bottom: 10px;
  right: 10px;
}
</style>
