<template>
  <div id="app" class="bg-dark-custom">
    <router-view/>
    <Footer />
  </div>
</template>

<script>
import Footer from '@/components/Footer.vue';

export default {
  name: 'App',
  components: {
    Footer
  }
}
// import { defineComponent } from '@vue/composition-api'

// export default defineComponent({
//   setup() {
//     return {}
//   },
// })
</script>
