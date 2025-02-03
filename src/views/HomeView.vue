<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'
import Observer from 'gsap/Observer'
import ScrollToPlugin from 'gsap/ScrollToPlugin'
import Lenis from 'lenis'

gsap.registerPlugin(ScrollTrigger)
gsap.registerPlugin(Observer)
gsap.registerPlugin(ScrollToPlugin)

const lenis = new Lenis({
  smoothWheel: true,
})
lenis.on('scroll', ScrollTrigger.update)
gsap.ticker.add((time) => {
  lenis.raf(time * 1000)
})
gsap.ticker.lagSmoothing(0)
const heroBg = ref()

onMounted(() => {
  gsap.fromTo(
    '.char',
    { y: '100%' },
    { y: 0, duration: 0.3, delay: 0.3, ease: 'power2.out', stagger: 0.018 },
  )
  if (window.innerWidth < 1024) {
    gsap.fromTo('.hero-p', { opacity: 0 }, { opacity: 1, duration: 0.3, delay: 0.6 })
  }
  gsap.fromTo('.hero-text', { y: '30%' }, { y: 0, duration: 0.5, delay: 1 })
  gsap.fromTo('.hero-bg', { autoAlpha: 0 }, { autoAlpha: 1, duration: 0.5, delay: 1 })
  const floatingEffect = gsap.to('.hero-bg', {
    y: 30,
    duration: 1,
    ease: 'power1.inOut',
    delay: 1.5,
    repeat: -1,
    yoyo: true,
  })
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: '.hero-bg',
      start: 'top 39.9%',
      end: 'center+=120 center',
      scrub: 1,
      onEnter: () => {
        floatingEffect.pause()
      },
      onLeaveBack: () => {
        floatingEffect.resume()
      },
    },
  })
  tl.to('.hero-bg', { scale: 2 })
  tl.to('.hero-bg', { opacity: 0 }, 0.1)

  gsap.to('.hero-text', {
    scrollTrigger: {
      trigger: '.hero-bg',
      start: 'top 38%',
      end: 'top 37%',
      scrub: 1,
    },
    opacity: 0,
  })

  const tl2 = gsap.timeline({
    scrollTrigger: {
      trigger: '.section-2',
      start: 'start center',
      end: 'center center',
      scrub: 1,
    },
  })
  tl2.from('.section-2', { opacity: 0, duration: 1.5 })
})
</script>

<template>
  <section class="section hero-section h-screen">
    <div
      ref="heroBg"
      class="absolute hero-bg z-[-1] h-[150dvh] w-full max-w-[1000px] min-w-[500px] top-[40vh] left-[50%] translate-x-[-50%] border-[6rem] border-b-0 md:border-[9rem] md:border-b-0 rounded-tl-[100%] rounded-tr-[100%] rounded-bl-[100%] rounded-br-[100%] border-[#000] blur-xl md:blur-2xl"
    ></div>
    <div class="flex flex-col h-full items-center justify-start text-black w-full hero-text">
      <h1
        class="w-full text-center max-w-[2000px] whitespace-nowrap font-bold mt-[120px] mb-1 lg:mb-auto leading-tight"
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
      <p
        class="text-center font-light text-black lg:text-[24px] mt-2 sm:mb-24 lg:text-white hero-p"
      >
        a creative digital studio<br />
        based in Maribor, Slovenia
      </p>
    </div>
  </section>
  <section class="section flex items-start justify-center">
    <div class="section-2 max-w-[500px] text-3xl">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Odio veritatis nulla sint alias
      asperiores inventore ut mollitia tenetur cumque possimus quibusdam maxime expedita a impedit,
      delectus placeat voluptatibus fugit accusantium!
    </div>
  </section>
  <section class="section h-[2000px]"></section>
</template>

<style scoped>
.hero-bg {
  will-change: opacity;
  background: radial-gradient(circle at 50% 50%, rgba(138, 43, 226, 0.1), rgba(138, 43, 226, 1));
}
.hero-text {
  will-change: opacity;
}
</style>
