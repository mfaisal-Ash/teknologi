<template>
  <div class="container-fluid p-0">
  <b-navbar toggleable="lg" type="dark" class="bg-dark-custom">
    <b-navbar-brand class="text-primary-custom" href="/">Diqtron</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item to="/">home</b-nav-item>
        <b-nav-item to="/menu" >Menu</b-nav-item>
      </b-navbar-nav>
      <b-navbar-nav class="ml-auto">
        <b-nav-item to="/keranjang">Keranjang
             <b-icon-bag></b-icon-bag>
             <span class="badge badge-light">0</span>
        </b-nav-item>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
  </div>
</template>

<script>
// import router from '@/router';

export default {
    name: 'NavbarView'
}
</script>

<style>

</style>