<script setup>
import NavBar from './components/NavBar.vue'
</script>

<template>
  <div>
    <NavBar />
    <main class="container my-5">
      <router-view />
    </main>
  </div>
</template>