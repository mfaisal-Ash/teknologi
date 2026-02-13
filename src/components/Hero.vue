<template>
  <!--Desktop View-->
  <div class="hero">
    <div class="d-none d-md-block">
      <div class="row mt-4">
        <div class="col-md-6 d-flex align-items-center">
          <div class="d-flex h-100">
             <div class="justify-content-center align-self-center">
              <h2 class="text-info-custom">
                Welcome to Diqtron. <br />
                <strong>Teknologi Menu, in Your Gadget.</strong>
              </h2>
              <p class="text-light mt-4">
                Silahkan dipilih dan pesan Teknologi favorit Anda.
              </p>
              <router-link
                to="/menu"
                class="btn btn-lg btn-success mt-3 text-primary-custom"
              >
                Pesan <b-icon-arrow-right />
              </router-link>
            </div>
          </div>
        </div>

        <!-- Image Column -->
        <div class="col-md-6 text-center">
          <img
            src="../assets/images/hero-img.png"
            alt="Delicious Food"
            width="100%"
          />
        </div>
      </div>
    </div>

    <!--Mobile View-->
    <div class="d-sm-blockl d-md-none">
      <div class="row mt-4">
        <!-- Image Column -->
        <div class="col-md-6 text-center">
          <img
            src="../assets/images/hero-img.png"
            alt="Delicious Food"
            width="100%"
          />
        </div>

        <div class="col-md-6 d-flex align-items-center">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2 class="text-info-custom">
                Welcome to Diqtron. <br />
                <strong>Teknologi Menu, in Your Gadget.</strong>
              </h2>
              <p class="text-light mt-4">
                Silahkan dipilih dan pesan Teknologi favorit Anda.
              </p>
              <router-link
                to="/menu"
                class="btn btn-lg btn-success mt-3 text-primary-custom"
              >
                Pesan <b-icon-arrow-right />
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeroView",
};
</script>

<style>
</style>