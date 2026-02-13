<template>
  <div class="fold-detail">
    <Navbar />

    <div class="container mt-4">

      <!-- Breadcrumb -->
      <b-breadcrumb :items="breadcrumbItems" class="mb-4" />

      <!-- LOADING -->
      <div v-if="loading" class="text-center text-light py-5">
        Loading...
      </div>

      <!-- ERROR -->
      <div v-else-if="error" class="text-center text-danger py-5">
        <h4>Produk tidak ditemukan</h4>
        <button class="btn btn-outline-info mt-3" @click="goBack">
          ← Kembali ke Menu
        </button>
      </div>

      <!-- CONTENT -->
      <div v-else class="row justify-content-center">
        <div class="col-12 col-sm-10 col-md-6 col-lg-4">

          <div class="menu-detail bg-dark text-white rounded-4 shadow-lg p-4">

            <!-- IMAGE -->
            <div class="text-center mb-4">
              <img
                :src="require('../assets/images/' + product.gambar)"
                class="product-img"
                alt="Product Image"
              />
            </div>

            <!-- INFO -->
            <h4 class="fw-bold text-center">
              {{ product.nama }}
            </h4>

            <p class="text-center text-success fs-5 mb-1">
              {{ formatRupiah(product.harga) }}
            </p>

            <p class="text-center text-warning mb-4">
              ⭐ {{ product.peringkat }}
            </p>

            <!-- FORM -->
            <div class="mb-3">
              <label class="form-label text-light">
                Jumlah Pesanan
              </label>
              <input
                type="number"
                class="form-control"
                v-model.number="quantity"
                min="1"
              />
            </div>

            <div class="mb-3">
              <label class="form-label text-light">
                Keterangan
              </label>
              <textarea
                class="form-control"
                rows="3"
                v-model="notes"
                placeholder="Tambahkan keterangan..."
              ></textarea>
            </div>

            <!-- BUTTON -->
            <div class="d-grid gap-2">
              <button class="btn btn-success btn-md ">
                Beli Sekarang <b-icon-cart />
              </button>

              <button
                class=" col-auto btn btn-outline-danger btn-md ml-3 h-100"
                @click="goBack"
              >
                ← Kembali
              </button>
            </div>

          </div>

        </div>
      </div>
    </div>
  </div>
</template>


<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "MenuDetail",
  components: { Navbar },

  data() {
  return {
    product: null,
    loading: true,
    error: false,
    quantity: 1,
    notes: "",
  };
},

  computed: {
    breadcrumbItems() {
      return [
        { text: "Home", active: true },
        { text: "Menu", active: true },
        {
          text: this.product ? this.product.nama : "Detail",
          active: true,
        },
      ];
    },
  },

  methods: {
    fetchProduct() {
      this.loading = true;
      this.error = false;

      axios
        .get(`http://localhost:3000/products/${this.$route.params.id}`)
        .then((res) => {
          this.product = res.data;
        })
        .catch(() => {
          this.error = true;
          this.product = null;
        })
        .finally(() => {
          this.loading = false;
        });
    },

    goBack() {
      this.$router.back();
    },

    formatRupiah(value) {
      return new Intl.NumberFormat("id-ID", {
        style: "currency",
        currency: "IDR",
      }).format(value);
    },
  },

  mounted() {
    this.fetchProduct();
  },

  watch: {
    "$route.params.id"() {
      this.fetchProduct();
    },
  },
};
</script>

<style>
.menu-detail {
  padding: 20px;
}
.menu-detail {
  background: #2f363d;
}

.product-img {
  max-width: 220px;
  width: 100%;
  border-radius: 16px;
  background: #fff;
  padding: 10px;
}

/* Mobile */
@media (max-width: 576px) {
  .menu-detail {
    padding: 16px;
  }
}

</style>