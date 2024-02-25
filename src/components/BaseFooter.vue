<script setup></script>

<template>
  <footer>
    <div class="text-light">Design in {{ new Date().getFullYear() }}</div>
  </footer>
</template>

<style scoped>
footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 56px;
  background-color: blue;
}
</style>
