<script setup lang="ts">
import { onMounted, ref } from 'vue'
import TheHeader from './components/TheHeader.vue'
import Lenis from 'lenis'

const isReady = ref(false)

onMounted(() => {
  const lenis = new Lenis({
    smoothWheel: true,
  })
  function raf(time: number) {
    lenis.raf(time)
    requestAnimationFrame(raf)
  }
  requestAnimationFrame(raf)
  setTimeout(() => {
    isReady.value = true
  }, 2000)
})
</script>

<template>
  <div v-if="isReady">
    <TheHeader />
    <router-view></router-view>
  </div>
</template>
