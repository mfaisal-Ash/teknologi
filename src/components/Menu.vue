<template>
  <div>
    <Navbar />

    <div class="container mt-4">
      <!-- Title -->
      <div class="row mb-4">
        <div class="col">
          <h1 class="text-light">Menu</h1>
        </div>
      </div>

      <div>
        <b-input-group size="sm" class="mb-4 w-50">
          <b-form-input
            v-model="searchQuery"
            type="search"
            placeholder="Search items"
            @keyup.enter="handleSearch"
          />
          <b-input-group-append
            is-text
            @click="handleSearch"
            style="cursor: pointer"
          >
            <b-icon icon="search" />
          </b-input-group-append>
        </b-input-group>
      </div>

      <!-- FILTER & SORT -->
      <div class="row mb-4 align-items-center">
        <div class="col-md-6 mb-2 mb-md-0">
          <div class="btn-group">
            <button
              class="btn btn-outline-info"
              :class="{ active: activeFilter === 'all' }"
              @click="setFilter('all')"
            >
              Semua
            </button>

            <button
              class="btn btn-outline-warning"
              :class="{ active: activeFilter === 'onSale' }"
              @click="setFilter('onSale')"
            >
              🔥 On Sale
            </button>

            <button
              class="btn btn-outline-success"
              :class="{ active: activeFilter === 'new' }"
              @click="setFilter('new')"
            >
              🆕 New
            </button>
          </div>
        </div>

        <div class="col-md-6 text-md-end">
          <select
            class="form-select w-auto d-inline"
            v-model="sortOrder"
            @change="fetchProducts"
          >
            <option value="">Urutkan Harga</option>
            <option value="asc">Termurah</option>
            <option value="desc">Termahal</option>
          </select>
        </div>
      </div>

      <!-- Product Grid -->
      <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-5 g-4">
        <div
          class="col d-flex"
          v-for="Product in products"
          :key="Product.id"
        >
          <CardProduct :product="Product" class="w-100" />
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import Navbar from "@/components/Navbar.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "MenuView",
  components: {
    Navbar,
    CardProduct,
  },

  data() {
    return {
      allProducts: [],     // data asli
      products: [],        // data hasil filter
      onSaleIds: [],
      newIds: [],
      searchQuery: "",
      activeFilter: "all", // all | onSale | new
      sortOrder: "",       // asc | desc
    };
  },

  methods: {
    async fetchInitialData() {
      try {
        const [productsRes, onSaleRes, newRes] = await Promise.all([
          axios.get("http://localhost:3000/products"),
          axios.get("http://localhost:3000/on-sale"),
          axios.get("http://localhost:3000/new-arrivals"),
        ]);

        this.allProducts = productsRes.data;

        // Simpan ID produk onSale & new
        this.onSaleIds = onSaleRes.data.map(p => p.nama);
        this.newIds = newRes.data.map(p => p.nama);

        this.applyFilter();
      } catch (err) {
        console.error("Fetch error:", err);
      }
    },

    applyFilter() {
      let result = [...this.allProducts];

      // FILTER
      if (this.activeFilter === "onSale") {
        result = result.filter(p =>
          this.onSaleIds.includes(p.nama)
        );
      }

      if (this.activeFilter === "new") {
        result = result.filter(p =>
          this.newIds.includes(p.nama)
        );
      }

      // SEARCH
      if (this.searchQuery) {
        result = result.filter(p =>
          p.nama.toLowerCase().includes(this.searchQuery.toLowerCase())
        );
      }

      // SORT
      if (this.sortOrder === "asc") {
        result.sort((a, b) => a.harga - b.harga);
      }

      if (this.sortOrder === "desc") {
        result.sort((a, b) => b.harga - a.harga);
      }

      this.products = result;
    },

    setFilter(filter) {
      this.activeFilter = filter;
      this.applyFilter();
    },

    handleSearch() {
      this.applyFilter();
    },
  },

  mounted() {
    this.fetchInitialData();
  },
};
</script>


<style>
</style>