<script setup lang="ts">
import { onMounted, ref } from 'vue'
const header = ref()

onMounted(() => {
  setTimeout(() => {
    header.value.style.transform = 'translateY(0)'
  }, 1000)
})
</script>

<template>
  <header
    ref="header"
    class="fixed z-50 top-4 left-4 right-4 flex items-center justify-between px-6 h-16 bg-white/30 backdrop-blur-[10px] rounded-[10px] shadow-[0_18px_40px_rgba(0,0,0,0.03),0_0_2px_rgba(0,0,0,0.14)] bg-blur max-w-[2000px] mx-auto"
  >
    <img src="../assets/logo.png" alt="logo" class="h-8 w-8" />
    <div class="hidden items-center gap-4 lg:flex">
      <router-link
        to="/"
        class="px-4 py-2 hover:bg-[#ededed] rounded-[10px]"
        activeClass="bg-[#ededed] rounded-[10px]"
      >
        <span class="leading-[18px]">Home</span>
      </router-link>
      <router-link
        to="/services"
        class="px-4 py-2 hover:bg-[#ededed] rounded-[10px]"
        activeClass="bg-[#ededed] rounded-[10px]"
      >
        <span class="leading-[18px]">What we do</span>
      </router-link>
      <router-link
        to="/about"
        class="px-4 py-2 hover:bg-[#ededed] rounded-[10px]"
        activeClass="bg-[#ededed] rounded-[10px]"
      >
        <span class="leading-[18px]">About</span>
      </router-link>
    </div>
    <div class="relative inline-flex group">
      <div
        class="absolute transitiona-all duration-1000 opacity-60 -inset-px bg-gradient-to-r from-[#8A2BE2] via-[#8A2BE2] to-[#8A2BE2] rounded-[10px] blur-md group-hover:opacity-80 group-hover:-inset-1 group-hover:duration-200 animate-tilt"
      ></div>
      <button
        type="button"
        class="relative inline-flex items-center justify-center px-4 py-2 text-white transition-all duration-200 bg-[#8A2BE2] rounded-[10px] focus:outline-none"
      >
        <span class="leading-[18px]">Let's work</span>
      </button>
    </div>
  </header>
</template>

<style scoped>
header {
  transform: translateY(-150px);
  transition: 0.5s;
}
</style>
