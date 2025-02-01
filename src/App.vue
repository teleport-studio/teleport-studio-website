<script setup lang="ts">
import { onMounted } from 'vue'
import TheHeader from './components/TheHeader.vue'
import Lenis from 'lenis'

onMounted(() => {
  const lenis = new Lenis()
  function raf(time: number) {
    lenis.raf(time)
    requestAnimationFrame(raf)
  }
  requestAnimationFrame(raf)
})
</script>

<template>
  <TheHeader />
  <RouterView />
</template>
