<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <p><strong>Current route path:</strong> {{ $route.fullPath }}</p>
  <nav class="flex gap-2">
    <RouterLink to="/" class="btn btn-primary">Go to Home</RouterLink>
    <RouterLink to="/about" class="btn btn-primary">Go to About</RouterLink>
  </nav>
  <RouterView />
</template>
