<script setup lang="ts">
import { nextTick, onBeforeUnmount, onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'
import Observer from 'gsap/Observer'
import ScrollToPlugin from 'gsap/ScrollToPlugin'
import Lenis from 'lenis'
import SplitType, { type TargetElement } from 'split-type'
// import { useBreakpoints } from '@vueuse/core'

// const breakpoints = useBreakpoints({ mobile: 1024 })

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
  nextTick(() => {})

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
      end: '60% 80%',
      scrub: 1,
      onEnter: () => {
        floatingEffect.pause()
      },
      onLeaveBack: () => {
        floatingEffect.resume()
      },
    },
  })
  tl.to('.hero-bg', { scale: 4 })
  // tl.to('.hero-bg', { opacity: 0 }, 0.1)

  gsap.to('.hero-text', {
    scrollTrigger: {
      trigger: '.hero-bg',
      start: 'top 36%',
      end: 'top 34%',
      scrub: 1,
    },
    opacity: 0,
  })

  const fadeTween = ref()
  ScrollTrigger.create({
    trigger: '.section-2',
    start: 'top 80%',
    onEnter: () => {
      if (fadeTween.value) fadeTween.value.kill()
      fadeTween.value = gsap.to('.section-2-text', {
        opacity: 1,
        duration: 1,
        ease: 'power1.inOut',
      })
    },
    onLeaveBack: () => {
      if (fadeTween.value) fadeTween.value.kill()
      fadeTween.value = gsap.to('.section-2-text', {
        opacity: 0,
        duration: 0.3,
        ease: 'power1.inOut',
      })
    },
  })

  const splitTypes = document.querySelectorAll('.scroll-highlight')
  splitTypes.forEach((char) => {
    const text = new SplitType(char as TargetElement, { types: ['chars', 'words'] })
    gsap.from(text.chars, {
      scrollTrigger: {
        trigger: char,
        start: 'top 80%',
        end: 'top 20%',
        scrub: true,
      },
      opacity: 0.2,
      stagger: 0.1,
    })
  })

  gsap.fromTo(
    '.animated-text',
    { yPercent: 100 },
    {
      yPercent: 0,
      duration: 0.8,
      ease: 'power4.out',
      scrollTrigger: {
        trigger: '.animated-text',
        start: 'top 85%',
        toggleActions: 'play none none none',
      },
    },
  )

  gsap.delayedCall(0.3, () => {
    ScrollTrigger.refresh()
  })

  gsap.fromTo(
    '.text-1',
    { xPercent: '-150' },
    {
      xPercent: '10',
      scrollTrigger: {
        trigger: '.text-1',
        start: 'top bottom',
        end: 'bottom top',
        scrub: true,
      },
    },
  )

  gsap.fromTo(
    '.text-2',
    { xPercent: '100' },
    {
      xPercent: '-40',
      scrollTrigger: {
        trigger: '.text-2',
        start: 'top bottom',
        end: 'bottom top',
        scrub: true,
      },
    },
  )
})

onBeforeUnmount(() => {
  ScrollTrigger.getAll().forEach((st) => st.kill())
})
</script>

<template>
  <section class="section hero-section h-[100svh]">
    <div
      ref="heroBg"
      class="hero-bg w-full max-w-[1000px] min-w-[500px] top-[40vh] border-[6rem] border-b-0 md:border-[9rem] md:border-b-0 rounded-tl-[100%] rounded-tr-[100%] rounded-bl-[100%] rounded-br-[100%] border-[#000] blur-xl md:blur-2xl"
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
        class="text-center font-light text-black text-sm lg:text-[18px] mt-2 sm:mb-24 lg:text-white hero-p"
      >
        a creative digital studio<br />
        based in Maribor, Slovenia
      </p>
    </div>
  </section>
  <section class="section-2">
    <div
      class="flex items-start justify-center max-w-[2000px] px-6 lg:px-12 xl:px-44 mx-auto section-2-text"
    >
      <div class="flex flex-col gap-6 lg:grid lg:gap-1.5 lg:grid-cols-12">
        <div class="lg:col-span-4">
          <h2 class="text-sm lg:text-[16px] uppercase mt-2">From the macro to the micro</h2>
        </div>
        <div class="flex flex-col gap-8 lg:col-span-8 text-left text-pretty">
          <span class="scroll-highlight text-2xl lg:text-[40px] xl:text-[50px] leading-[1.25]">
            At Teleport Studio, we believe every project is a unique story waiting to be told. We
            focus on transforming your vision into a digital experience that feels both authentic
            and thoughtfully crafted.
          </span>
          <span class="text-sm lg:text-[18px] overflow-hidden">
            <span class="block animated-text">
              We take the time to listen to your ideas and understand your values, ensuring that
              every detail reflects who you are. Together, we create a digital space that not only
              captures your identity but also resonates with your audience.
            </span>
          </span>
        </div>
      </div>
    </div>
  </section>
  <section class="section-3 overflow-hidden">
    <div class="flex flex-col sliding-text pt-20 py-14 lg:py-40 xl:py-64">
      <span class="inline-block whitespace-nowrap text-[17vw] text-1 leading-[1]"
        >We set the bar high</span
      >
      <span class="inline-block whitespace-nowrap text-[17vw] text-2 leading-[1] text-white"
        >for our projects</span
      >
    </div>
  </section>
  <section class="section-4 h-[2000px] bg-[#161618] relative"></section>
</template>

<style scoped>
.hero-bg {
  will-change: opacity, transform, translateX;
  position: absolute;
  z-index: -1;
  height: 150dvh;
  left: 50%;
  -webkit-transform: translateX(-50%);
  transform: translateX(-50%);
  background: radial-gradient(circle at 50% 50%, rgba(138, 43, 226, 0.1), rgba(138, 43, 226, 1));
}
.hero-text {
  will-change: opacity;
}
.scroll-highlight {
  font-family: 'Hedvig Letters Serif';
}
.section-2-text {
  opacity: 0;
}
.sliding-text > span {
  will-change: transform, translateX;
  font-family: 'Hedvig Letters Serif';
}

.section-4:before {
  content: '';
  background-color: transparent;
  background-image: url('../assets/noise.svg');
  background-repeat: repeat;
  background-size: 600px;
  opacity: 0.1;
  top: 0;
  left: 0;
  position: absolute;
  width: 100%;
  height: 100%;
}
</style>
