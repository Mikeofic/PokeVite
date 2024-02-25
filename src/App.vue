<script setup>
import BaseFooter from "./components/BaseFooter.vue";
import BaseNavbar from "./components/BaseNavbar.vue";
</script>

<template>
  <BaseNavbar />
  <div class="main"><RouterView /></div>
  <BaseFooter />
</template>

<style>
body {
  height: 100vh;
  overflow-x: hidden;
}
</style>
