<template>
  <div class="home">
<Header/>
<Body/>
<Footer/>
  </div>
</template>

<script>

import Header from '../components/header.vue'
import Footer from '../components/Footer.vue'
import Body from '../components/Body.vue'
export default {
  name: 'Home',
  components: {
    Header,
    Footer,
    Body
  }
}
</script>
