<script setup lang="ts">
import { computed, onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { usePointer } from '@vueuse/core'

const { x, y } = usePointer()

const heroBg = ref()

const transformBg = computed(() => {
  const offsetX = (x.value - window.innerWidth / 2) * 0.04
  const offsetY = (y.value - window.innerHeight / 2) * 0.04

  return `translate3d(${offsetX}px, ${offsetY}px, 0)`
})

onMounted(() => {
  gsap.to('.char', {
    duration: 0.1,
    y: 0,
    delay: 0.1,
    stagger: 0.015,
  })
  gsap.to('.hero-text', {
    duration: 0.1,
    y: 0,
    delay: 1,
  })
  gsap.fromTo(
    heroBg.value,
    { opacity: 0 },
    {
      opacity: 1,
      duration: 1,
      delay: 1,
      ease: 'power2.out',
    },
  )
})
</script>

<template>
  <section class="h-svh">
    <div
      ref="heroBg"
      class="absolute z-[-1] h-[150vh] w-full max-w-[1000px] min-w-[500px] top-[40vh] left-[50%] translate-x-[-50%] border-[6rem] border-b-0 md:border-[9rem] md:border-b-0 rounded-tl-[100%] rounded-tr-[100%] rounded-bl-[100%] rounded-br-[100%] border-[#000] blur-xl md:blur-2xl"
      :style="{ transform: transformBg }"
    ></div>
    <div class="flex flex-col h-full items-center justify-start text-black w-full hero-text">
      <h1
        class="w-full text-center max-w-[2000px] whitespace-nowrap font-bold mt-[120px] mb-auto leading-tight"
        style="font-size: clamp(2rem, 12vw, 16rem)"
        :style="{
          clipPath: 'polygon(0 0, 100% 0, 100% 100%, 0 100%)',
        }"
      >
        <div class="inline-block char">T</div>
        <div class="inline-block char">e</div>
        <div class="inline-block char">l</div>
        <div class="inline-block char">e</div>
        <div class="inline-block char">p</div>
        <div class="inline-block char">o</div>
        <div class="inline-block char">r</div>
        <div class="inline-block char">t</div>
        <div class="inline-block char">&nbsp;</div>
        <div class="inline-block char">S</div>
        <div class="inline-block char">t</div>
        <div class="inline-block char">u</div>
        <div class="inline-block char">d</div>
        <div class="inline-block char">i</div>
        <div class="inline-block char">o</div>
      </h1>
      <p class="text-center font-extralight lg:text-[20px] mb-[10%]">
        a creative digital studio<br />
        based in Maribor, Slovenia
      </p>
    </div>
  </section>
  <section class="h-[2000px]"></section>
</template>

<style scoped>
.char {
  transform: translateY(13vw);
  transition: transform 0.3s;
}
.hero-text {
  transform: translateY(30%);
  transition: transform 0.5s;
}
</style>
