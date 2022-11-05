

<template>
  <div class="container">
    <Header title="Task Tracker" @toggle-add-task="toggleAddTask" :showAddTask='showAddTask' />
   <!-- //sending props in routing -->
    <router-view :showAddTask="showAddTask"></router-view>
    <Footer />
  </div>
</template>
<!-- ================================= -->
<script>
import Header from "./components/Header";
import Footer from "./components/Footer";

export default {
  name: "App",
  components: {
    Header,
    Footer
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
  },
  data() {
    return {
     showAddTask: false
    };
  }
};
</script>
<!-- ================================== -->

<style>
@import "./assets/css/style.css";
</style>
