<template>
  <div class="Cart">
    <Navbar />
    <!-- Breadcrumb -->
      <b-breadcrumb :items="breadcrumbItems" class="mb-4" />
    <h1>Cart Component</h1>
    
  </div>
</template>

<script>
export default {
    name: 'CartView',
    components: {
      Navbar,  
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
}
</script>

<style>

</style>