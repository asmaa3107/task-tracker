

<template>
  <div class="container">
    <Header title="Task Tracker"/>
    <Footer />
  </div>
</template>
<!-- ================================= -->
<script>
import Header from './components/Header'
import Footer from './components/Footer'
export default {
  name: 'App',
  components: {
    Header,
    Footer
  }
}
</script>
<!-- ================================== -->

<style>
  @import './assets/css/style.css';
</style>
