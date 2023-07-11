<template>
  <div class="home">
    <Navbar />
    <Hero />
    <div class="grid grid-cols-2 px-11">
      <h2 class="mt-3 text-2xl"><span class="font-bold">Sepatu</span> The Best</h2>
      <router-link to="/products" class="btn btn-sm btn-success justify-self-end mt-3">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
          <path fill-rule="evenodd"
            d="M3.75 12a.75.75 0 01.75-.75h13.19l-5.47-5.47a.75.75 0 011.06-1.06l6.75 6.75a.75.75 0 010 1.06l-6.75 6.75a.75.75 0 11-1.06-1.06l5.47-5.47H4.5a.75.75 0 01-.75-.75z"
            clip-rule="evenodd" />
        </svg>
        Lihat Semua
      </router-link>
    </div>

    <!-- grid top product -->
    <div class="grid md:grid-cols-3 sm:grid-cols-1 gap-2 md:gap-2 sm:gap-1 justify-center px-4">
      <div class="px-1 justify-self-center" v-for="product in products" :key="product.id">
        <Card :product="product" />
      </div>
    </div>

  </div>
</template>

<script >
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import Hero from '@/components/Hero.vue'
import Card from '@/components/Card.vue'
import axios from 'axios'

export default {
  name: 'HomeView',
  components: {
    Navbar,
    Hero,
    Card
  },
  data() {
    return {
      products: []
    }
  },
  methods: {
    setProduct(data) {
      this.products = data
    },
    async getBestProduct() {
      await axios.get('http://localhost:3000/best_sepatu')
        .then((res) => {
          this.setProduct(res.data)
        }).catch((err) => {
          console.log(err)
        })
    }
  },
  mounted() {
    this.getBestProduct()
  }
}

</script>
