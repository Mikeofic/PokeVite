<script setup>
import NavToogle from "./NavToogle.vue";
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
    <div class="container-fluid">
      <RouterLink class="navbar-brand" to="/">
        <img
          src="./assets/icon.svg"
          alt=""
          height="40"
          class="d-inline-block align-text-center"
        />
        PokeVite
      </RouterLink>

      <NavToogle />
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <RouterLink class="nav-link" to="/">Home</RouterLink>
          </li>
          <li class="nav-item">
            <RouterLink class="nav-link" to="/about">About</RouterLink>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
