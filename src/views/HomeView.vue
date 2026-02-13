<template>
  <div class="home">
    <Navbar />
    <div class="container">
      <Hero />
      <div class="row mb-4">
        <div class="col text-center">
          <h2 class="text-info-custom">Featured Menu</h2>
          <p class="text-light mb-4">
            Discover our delicious featured dishes, handpicked just for you!
          </p>
        </div>
      </div>

      <!-- Featured Menu Items will go here -->
      <div class="row align-items-center mb-4">
        <div class="col-12 col-md-6">
          <h3 class="text-light fw-bold mb-2 mb-md-0">
            Best <span class="text-info">Products</span>
          </h3>
        </div>

        <!--button to view all menu items -->
        <div class="col text-end">
          <router-link
            to="/menu"
            class="btn btn-info d-inline-flex align-items-center float-right gap-2"
          >
            Lihat semuanya<b-icon-eye
          /></router-link>
        </div>
      </div>

      <div class="row mb-4">
        <div
          class="col-md-4 mt-4"
          v-for="Product in products"
          :key="Product.id"
        >
          <!-- <h2 class="text-light">Technology</h2> -->
          <CardProduct :product="Product" />
        </div>
      </div>

      <!-- Footer Section -->
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

import Navbar from "@/components/Navbar.vue";
import Hero from "@/components/Hero.vue";
import CardProduct from "@/components/CardProduct.vue";
// import Footer from '@/components/Footer.vue';
import axios from "axios";
export default {
  name: "HomeView",
  components: {
    Navbar,
    Hero,
    CardProduct,
  },
  data() {
    return {
      products: [],
    };
  },
  methods: {
    setProduct(data) {
      this.products = data;
    },
  },
 mounted() {
  Promise.all([
    axios.get("http://localhost:3000/products?_limit=5"),
    axios.get("http://localhost:3000/products?onSale=true&_limit=5"),
    axios.get("http://localhost:3000/products?new=true&_limit=5"),
  ])
    .then(([all, onSale, newest]) => {
      this.products = all.data;
      this.onSaleProducts = onSale.data;
      this.newProducts = newest.data;
    })
    .catch((err) => {
      console.error("Fetch error:", err);
    })
    .finally(() => {
      this.loading = false;
    });
},
  // methods: {
  //   fetchProducts(){
  //     fetch('http://localhost:3000/products')
  //     .then(response => response.json())
  //     .then(data => {
  //       this.products = data;
  //     })
  //     .catch(error => {
  //       console.error('Error fetching products:', error);
  //     });
  //   }
  // },
};
</script>
