<script setup>
import Navbar from "./components/Navbar.vue";
import { RouterView } from "vue-router";
</script>
<template>
  <main class="flex flex-col justify-stretch">
    <Navbar />
    <RouterView />
  </main>
</template>