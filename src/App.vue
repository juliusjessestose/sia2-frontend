<script setup>
import { RouterLink, RouterView } from "vue-router";
import NavBar from "./components/NavBar.vue";
import Footer from "./views/Footer.vue";
</script>

<template>
  <NavBar />

  <RouterView />
  <!-- <Footer /> -->
</template>

<style>
#app {
  height: 100vh;
}
.hover-links:hover {
  color: white;
}
</style>
