<script setup lang="ts">
import { useCounterStore } from '@/stores/counter'
const counter = useCounterStore()
</script>

<template>
  <h3 class="text-2xl">Home</h3>

  <p>Count: {{ counter.count }}</p>
  <p>Double Count: {{ counter.doubleCount }}</p>
  <button class="btn btn-secondary" @click="counter.increment">Increment</button>
</template>
