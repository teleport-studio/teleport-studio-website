<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)
const heroBg = ref()

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
  // gsap.to(heroBg.value, {
  //   scale: 1.5, // Scale up the div
  //   duration: 2,
  //   scrollTrigger: {
  //     trigger: heroBg.value,
  //     start: "top bottom", // Animation starts when the top of div enters the viewport
  //     end: "top center", // Ends when div reaches center of viewport
  //     scrub: 1, // Smooth scrubbing effect
  //   },
  // });
})
</script>

<template>
  <section class="h-svh">
    <div
      ref="heroBg"
      class="absolute hero-bg z-[-1] h-[150vh] w-full max-w-[1000px] min-w-[500px] top-[40vh] left-[50%] translate-x-[-50%] border-[6rem] border-b-0 md:border-[9rem] md:border-b-0 rounded-tl-[100%] rounded-tr-[100%] rounded-bl-[100%] rounded-br-[100%] border-[#000] blur-xl md:blur-2xl"
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
      <p class="text-center font-extralight text-white lg:text-[20px] mb-[10%]">
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
@keyframes float {
  0% {
    transform: translatey(0);
  }
  50% {
    transform: translatey(6vh);
  }
  100% {
    transform: translatey(0);
  }
}
.hero-bg {
  animation: float 3s ease-in-out infinite;
  background: radial-gradient(circle at 50% 50%, rgba(138, 43, 226, 0.1), rgba(138, 43, 226, 1));
  opacity: 0.2;
}
</style>
