<template>
  <div>
  <Navbar />
  <div class="section">
  <router-view/>
  </div>
  <Footer />
  </div>
  
</template>

<style lang="scss">

@import '../node_modules/bulma';
</style>
<script>
import Footer from './components/Footer.vue'
import Navbar from './components/Navbar.vue'
export default {
  name:'App',
  components:{
    Navbar,Footer
  }
}
</script>
