<template>
  <div>
    <Navbar />
    <main>
      <div class="container">
        <Nuxt />
      </div>
    </main>
  </div>
</template>

<script>
import Vue from 'vue'
import Navbar from '~/components/Navbar.vue'
export default Vue.extend({
  components: {
    Navbar,
  },
})
</script>
