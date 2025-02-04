<script setup lang="ts">
import { onMounted, ref, watch } from 'vue'
import { useRouter } from 'vue-router'
import { gsap } from 'gsap'
import { vOnClickOutside } from '@vueuse/components'

const router = useRouter()
const header = ref()
const menu = ref(false)

const toggleMenu = () => {
  menu.value = !menu.value
}

onMounted(async () => {
  await router.isReady()
  if (router.currentRoute.value.path === '/') {
    gsap.fromTo(header.value, { y: -150 }, { y: 0, duration: 0.5, delay: 0.5, ease: 'power2.out' })
  }
})

watch(
  () => router.currentRoute.value.path,
  (newPath) => {
    if (newPath === '/') {
      gsap.fromTo(
        header.value,
        { y: -150 },
        { y: 0, duration: 0.5, delay: 0.5, ease: 'power2.out' },
      )
    }
  },
)
watch(
  () => menu.value,
  (newPath) => {
    if (newPath) {
      gsap.fromTo('.mobile-menu', { opacity: 0 }, { opacity: 1, duration: 0.5, ease: 'power2.out' })
    } else {
      gsap.fromTo('.mobile-menu', { opacity: 1 }, { opacity: 0, duration: 0.5, ease: 'power2.out' })
    }
  },
)
</script>

<template>
  <header
    ref="header"
    class="fixed z-50 top-4 left-4 right-4 h-16 flex flex-col justify-start lg:justify-center bg-white/30 backdrop-blur-[10px] rounded-[10px] shadow-[0_18px_40px_rgba(0,0,0,0.03),0_0_2px_rgba(0,0,0,0.14)] bg-blur max-w-[2000px] translate-y-[-150px] transition-all duration-500 overflow-hidden"
    :class="{ 'h-[328.5px]': menu }"
    v-on-click-outside="() => (menu = false)"
  >
    <div class="flex items-center justify-between px-4 pt-4 lg:pt-0 lg:px-6">
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
      <div class="hidden lg:inline-flex relative group">
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
      <div
        id="toggleMenu"
        @click="toggleMenu()"
        class="grid lg:hidden place-content-center w-8 h-8"
        :class="{
          '[&>div]:h-0 [&>div]:bg-white [&>div]:before:translate-y-0 [&>div]:before:rotate-45 [&>div]:after:translate-y-0 [&>div]:after:-rotate-45':
            menu,
        }"
      >
        <div
          class="w-6 h-[2px] bg-black transition-all duration-150 before:content-[''] before:absolute before:w-6 before:h-[2px] before:bg-black before:-translate-y-2 before:transition-all before:duration-150 after:content-[''] after:absolute after:w-6 after:h-[2px] after:bg-black after:translate-y-2 after:transition-all after:duration-150"
        ></div>
      </div>
    </div>
    <div class="mobile-menu flex flex-col gap-3 px-4 pb-4 py-4 items-center lg:hidden">
      <router-link
        to="/"
        @click="toggleMenu()"
        class="px-4 py-2 rounded-[10px] w-full text-center"
        activeClass="bg-black text-center text-white"
      >
        <span class="text-xl">Home</span>
      </router-link>
      <router-link
        to="/services"
        @click="toggleMenu()"
        class="px-4 py-2 rounded-[10px] w-full text-center"
        activeClass="bg-black text-center text-white"
      >
        <span class="text-xl">What we do</span>
      </router-link>
      <router-link
        to="/about"
        @click="toggleMenu()"
        class="px-4 py-2 rounded-[10px] w-full text-center"
        activeClass="bg-black text-center text-white"
      >
        <span class="text-xl">About</span>
      </router-link>
      <hr class="border-t-[0.5px] border-[#888] w-full my-3" />
      <div class="inline-flex relative group w-full">
        <div
          class="absolute transitiona-all duration-1000 opacity-60 -inset-px bg-gradient-to-r from-[#8A2BE2] via-[#8A2BE2] to-[#8A2BE2] rounded-[10px] blur-md group-hover:opacity-80 group-hover:-inset-1 group-hover:duration-200 animate-tilt"
        ></div>
        <button
          type="button"
          class="relative inline-flex items-center justify-center px-4 py-2 w-full text-white transition-all duration-200 bg-[#8A2BE2] rounded-[10px] focus:outline-none"
        >
          <span class="text-xl">Let's workk</span>
        </button>
      </div>
    </div>
  </header>
</template>
