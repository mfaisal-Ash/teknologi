<template>
  <div class="card product-card h-100 bg-dark text-white shadow rounded-4 d-flex flex-column">

    <!-- IMAGE -->
    <div class="product-img-wrapper">
      <img
        :src="require('../assets/images/' + product.gambar)"
        class="product-img"
        alt="Product"
      />
    </div>

    <!-- BODY -->
    <div class="card-body d-flex flex-column px-3">

      <h6 class="card-title fw-semibold text-center mb-1">
        {{ product.nama }}
      </h6>

      <small class="text-warning text-center mb-2">
        ⭐ {{ product.peringkat }}
      </small>

      <p class="fw-bold text-success text-center mb-3">
        Rp {{ product.harga }}
      </p>

      <!-- BUTTON -->
      <div class="mt-auto">
        <router-link
          :to="'/menu/' + product.id"
          class="btn btn-secondary w-100 btn-sm"
        >
          Pesan <b-icon-cart />
        </router-link>
      </div>

    </div>
  </div>
</template>


<script>
export default {
    name: 'CardProduct',
    props: ['product']
}
</script>

<style>

</style>