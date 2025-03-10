<script setup lang="ts">
import { nextTick, onBeforeUnmount, onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'
import Observer from 'gsap/Observer'
import ScrollToPlugin from 'gsap/ScrollToPlugin'
import Lenis from 'lenis'
import SplitType, { type TargetElement } from 'split-type'

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

const cardsRef = ref<HTMLElement | null>(null)

const handleMouseMoveSection5 = (e: MouseEvent) => {
  if (!cardsRef.value) return

  const cards = cardsRef.value.querySelectorAll('.card')

  cards.forEach((card) => {
    const rect = card.getBoundingClientRect()
    const x = e.clientX - rect.left
    const y = e.clientY - rect.top

    card.style.setProperty('--mouse-x', `${x}px`)
    card.style.setProperty('--mouse-y', `${y}px`)
  })
}

onMounted(() => {
  nextTick(() => {})

  if (cardsRef.value) {
    cardsRef.value.addEventListener('mousemove', handleMouseMoveSection5)
  }

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
  tl.to('.hero-bg', { opacity: 0 }, 0.1)

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

  //section 4
  const splitTypes4 = document.querySelectorAll('.scroll-highlight-4-1')
  splitTypes4.forEach((char) => {
    const text = new SplitType(char as TargetElement, { types: ['chars', 'words'] })
    gsap.from(text.chars, {
      scrollTrigger: {
        trigger: char,
        start: 'top 90%',
        end: 'top 20%',
        scrub: true,
      },
      opacity: 0.2,
      stagger: 0.1,
    })
  })

  gsap.fromTo(
    '.animated-text-4-1',
    { yPercent: 100 },
    {
      yPercent: 0,
      duration: 0.8,
      ease: 'power4.out',
      scrollTrigger: {
        trigger: '.animated-text-4-1',
        start: 'top 85%',
        toggleActions: 'play none none none',
      },
    },
  )

  gsap.fromTo(
    ['.service-card-1', '.service-card-2', '.service-card-3'],
    { opacity: 0, y: 100 },
    {
      opacity: 1,
      y: 0,
      duration: 0.5,
      stagger: 0.2,
      ease: 'power4.out',
      scrollTrigger: {
        trigger: '.service-card-1',
        start: 'top 80%',
      },
    },
  )

  //section 5
  const splitTypes5 = document.querySelectorAll('.scroll-highlight-5')
  splitTypes5.forEach((char) => {
    const text = new SplitType(char as TargetElement, { types: ['chars', 'words'] })
    gsap.from(text.chars, {
      scrollTrigger: {
        trigger: char,
        start: 'top 90%',
        end: 'top 20%',
        scrub: true,
      },
      opacity: 0.2,
      stagger: 0.1,
    })
  })
})

onBeforeUnmount(() => {
  ScrollTrigger.getAll().forEach((st) => st.kill())
  if (cardsRef.value) {
    cardsRef.value.removeEventListener('mousemove', handleMouseMoveSection5)
  }
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
      <!-- <div class="flex text-center flex-col gap-6">
        <div class="">
          <h2 class="text-sm lg:text-[16px] uppercase mt-2">From the macro to the micro</h2>
        </div>
        <div class="flex flex-col gap-8 lg:col-span-8 text-left text-pretty">
          <span class="scroll-highlight text-2xl lg:text-[30px] leading-[1.25] text-center">
            At Teleport Studio, we believe every project is a unique story waiting to be told. We
            focus on transforming your vision into a digital experience that feels both authentic
            and thoughtfully crafted.
          </span>
        </div>
      </div> -->
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
          <span class="text-sm lg:text-[18px] font-[300] overflow-hidden">
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
      <span class="inline-block whitespace-nowrap text-[17vw] text-2 leading-[1] text-[#48348B]"
        >for our projects</span
      >
    </div>
  </section>
  <section class="section-4 bg-[#161618] pt-14 lg:pt-64 xl:pt-72">
    <div class="section-4-1 flex items-center justify-center relative">
      <div class="flex items-start justify-center max-w-[2000px] px-6 lg:px-12 xl:px-44 mx-auto">
        <div class="flex flex-col gap-6 lg:grid lg:gap-1.5 lg:grid-cols-12 w-full">
          <div class="lg:col-span-4">
            <h2 class="text-sm lg:text-[16px] w-fit uppercase mt-2 text-white">What we do</h2>
          </div>
          <div class="flex flex-col gap-6 lg:col-span-8 text-left text-pretty">
            <span class="scroll-highlight-4-1 text-white text-2xl lg:text-[40px] leading-[1.25]">
              We are dedicated to turning your ideas into reality. Our goal is to create engaging
              digital experiences that empower your business to achieve its goals.
            </span>
            <span class="text-sm lg:text-[18px] font-[100] overflow-hidden">
              <span class="block text-white animated-text-4-1">
                We also specialize in custom solutions designed just for you. By working closely
                with you, we build tailor-made software products that address your specific needs.
              </span>
            </span>
          </div>
        </div>
      </div>
    </div>
    <div class="section-4-2 py-28 lg:py-40 xl:py-64 relative">
      <div class="flex flex-col gap-6 lg:gap-20">
        <div class="w-full max-w-[2000px] px-6 lg:px-12 xl:px-44 mx-auto">
          <h2 class="text-sm lg:text-[16px] w-fit uppercase text-white">AND FOR THAT WE OFFER</h2>
        </div>
        <div
          class="flex flex-col w-full lg:flex-row items-stretch gap-10 max-w-[2000px] px-6 lg:px-12 xl:px-12 2xl:px-44 mx-auto"
        >
          <div
            class="service-card-1 flex flex-col w-full bg-[#1F1F21] rounded-2xl p-5 lg:p-8 relative"
          >
            <h2 class="mb-6 lg:mb-8 text-3xl lg:text-4xl text-white">
              <span class="text-[#48348B]">WEB</span><br />DEVELOPMENT
            </h2>
            <ul class="list-disc list-inside text-[#d1d1d1] text-sm lg:text-base">
              <li>Complete custom website experiences</li>
              <li>Custom ecommerce solutions</li>
              <li>Powerful CMS integrations</li>
              <li>Branded email templates</li>
              <li>Mobile-optimized websites</li>
              <li>Seamless website deployment</li>
              <li>Maintenance & support</li>
            </ul>
            <span
              class="card-number hidden lg:block absolute bottom-8 right-8 text-[#48348B] opacity-30 text-8xl leading-16"
              >01</span
            >
          </div>
          <div
            class="service-card-2 flex flex-col w-full bg-[#1F1F21] rounded-2xl p-5 lg:p-8 relative"
          >
            <h2 class="mb-6 lg:mb-8 text-3xl lg:text-4xl text-white">
              <span class="text-[#48348B]">UX/UI</span><br />DESIGN
            </h2>
            <ul class="list-disc list-inside text-[#d1d1d1] text-sm lg:text-base">
              <li>Beautiful & easy-to-use designs</li>
              <li>Custom layouts for your brand</li>
              <li>Mobile-friendly experiences</li>
              <li>Fast & smooth interactions</li>
              <li>Eye-catching animations</li>
              <li>Consistent design across platforms</li>
              <li>Ongoing design improvements</li>
            </ul>
            <span
              class="card-number hidden lg:block absolute bottom-8 right-8 text-[#48348B] opacity-30 text-8xl leading-16"
            >
              02
            </span>
          </div>
          <div
            class="service-card-3 flex flex-col w-full bg-[#1F1F21] rounded-2xl p-5 lg:p-8 relative"
          >
            <h2 class="mb-6 lg:mb-8 text-3xl lg:text-4xl text-white">
              <span class="text-[#48348B]">DIGITAL</span><br />BRANDING
            </h2>
            <ul class="list-disc list-inside text-[#d1d1d1] text-sm lg:text-base">
              <li>Social media branding & management</li>
              <li>High-converting ad creatives</li>
              <li>Engaging content marketing</li>
              <li>SEO & performance marketing</li>
              <li>Photography & video3 production</li>
            </ul>
            <span
              class="card-number hidden lg:block absolute bottom-8 right-8 text-[#48348B] opacity-30 text-8xl leading-16"
            >
              03
            </span>
          </div>
        </div>
      </div>
    </div>
  </section>
  <section class="section-5 flex flex-col items-center bg-[#161618] pb-14 lg:pb-64 xl:pb-72">
    <h2 class="text-sm lg:text-[16px] w-fit uppercase text-white">SO WHY CHOOSE US ?</h2>
    <p
      class="text-white text-2xl scroll-highlight-5 text-pretty lg:text-[40px] leading-[1.25] text-center max-w-[1250px] px-6 lg:px-12 mt-6 mb-16 lg:mb-28 lg:mt-20"
    >
      We're a small team of passionate creators who love what we do. Every project is personal, and
      we work closely with you to bring your vision to life.
    </p>
    <div ref="cardsRef" id="cards">
      <div class="card">
        <div class="card-content">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            stroke-width="1"
            class="w-16 h-16"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M21 8.25c0-2.485-2.099-4.5-4.688-4.5-1.935 0-3.597 1.126-4.312 2.733-.715-1.607-2.377-2.733-4.313-2.733C5.1 3.75 3 5.765 3 8.25c0 7.22 9 12 9 12s9-4.78 9-12Z"
            />
          </svg>
          <h2 class="text-white text-2xl mb-3 mt-10">Crafted with Love</h2>
          <span class="text-[#a4a4a4] text-sm text-center max-w-60">
            We love what we do, and it shows in our work. Every project is crafted with care.
          </span>
        </div>
      </div>
      <div class="card">
        <div class="card-content">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            stroke-width="1"
            class="w-16 h-16"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M9 9V4.5M9 9H4.5M9 9 3.75 3.75M9 15v4.5M9 15H4.5M9 15l-5.25 5.25M15 9h4.5M15 9V4.5M15 9l5.25-5.25M15 15h4.5M15 15v4.5m0-4.5 5.25 5.25"
            />
          </svg>
          <h2 class="text-white text-2xl mb-3 mt-10">Focused on You</h2>
          <span class="text-[#a4a4a4] text-sm text-center max-w-60">
            We listen to your needs and create solutions that fit you perfectly.
          </span>
        </div>
      </div>
      <div class="card">
        <div class="card-content">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            stroke-width="1"
            class="w-16 h-16"
          >
            <path
              fill-rule="evenodd"
              d="M9 4.5a.75.75 0 0 1 .721.544l.813 2.846a3.75 3.75 0 0 0 2.576 2.576l2.846.813a.75.75 0 0 1 0 1.442l-2.846.813a3.75 3.75 0 0 0-2.576 2.576l-.813 2.846a.75.75 0 0 1-1.442 0l-.813-2.846a3.75 3.75 0 0 0-2.576-2.576l-2.846-.813a.75.75 0 0 1 0-1.442l2.846-.813A3.75 3.75 0 0 0 7.466 7.89l.813-2.846A.75.75 0 0 1 9 4.5ZM18 1.5a.75.75 0 0 1 .728.568l.258 1.036c.236.94.97 1.674 1.91 1.91l1.036.258a.75.75 0 0 1 0 1.456l-1.036.258c-.94.236-1.674.97-1.91 1.91l-.258 1.036a.75.75 0 0 1-1.456 0l-.258-1.036a2.625 2.625 0 0 0-1.91-1.91l-1.036-.258a.75.75 0 0 1 0-1.456l1.036-.258a2.625 2.625 0 0 0 1.91-1.91l.258-1.036A.75.75 0 0 1 18 1.5ZM16.5 15a.75.75 0 0 1 .712.513l.394 1.183c.15.447.5.799.948.948l1.183.395a.75.75 0 0 1 0 1.422l-1.183.395c-.447.15-.799.5-.948.948l-.395 1.183a.75.75 0 0 1-1.422 0l-.395-1.183a1.5 1.5 0 0 0-.948-.948l-1.183-.395a.75.75 0 0 1 0-1.422l1.183-.395c.447-.15.799-.5.948-.948l.395-1.183A.75.75 0 0 1 16.5 15Z"
              clip-rule="evenodd"
            />
          </svg>
          <h2 class="text-white text-2xl mb-3 mt-10">Creative Touch</h2>
          <span class="text-[#a4a4a4] text-sm text-center max-w-60">
            Our young team brings innovative and modern designs that stand out.
          </span>
        </div>
      </div>
      <div class="card">
        <div class="card-content">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            stroke-width="1"
            class="w-16 h-16"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M9 12.75 11.25 15 15 9.75m-3-7.036A11.959 11.959 0 0 1 3.598 6 11.99 11.99 0 0 0 3 9.749c0 5.592 3.824 10.29 9 11.623 5.176-1.332 9-6.03 9-11.622 0-1.31-.21-2.571-.598-3.751h-.152c-3.196 0-6.1-1.248-8.25-3.285Z"
            />
          </svg>
          <h2 class="text-white text-2xl mb-3 mt-10">Trust & Collaboration</h2>
          <span class="text-[#a4a4a4] text-sm text-center max-w-60">
            We work closely with you to make sure your vision comes to life exactly as you imagined.
          </span>
        </div>
      </div>
    </div>
  </section>
  <footer class="flex items-center justify-between relative p-40">
    <p class="max-w-[314px]">
      We'd love to hear from you. Whether you have a question or a project in mind, we're here to
      help.
    </p>
    <div class="flex flex-col items-end">
      <h2 class="text-3xl text-[]">Let's work</h2>
      <a
        href="mailto:info@teleport-studio.com"
        class="text-[3em] hover:underline hover:text-[#48348B] transition-colors duration-500"
      >
        info@teleport-studio.com
      </a>
    </div>
    <small class="absolute bottom-2 right-2">&copy; 2025 TELEPORT STUDIO</small>
  </footer>
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
.scroll-highlight,
.scroll-highlight-4-1 {
  font-family: 'Hedvig Letters Serif';
}
.section-2-text {
  opacity: 0;
}
.sliding-text > span {
  will-change: transform, translateX;
  font-family: 'Hedvig Letters Serif';
}

.card-number {
  font-family: 'Hedvig Letters Serif';
}

/* .section-4::before {
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
  pointer-events: none;
} */

.section-5 {
  p {
    font-family: 'Hedvig Letters Serif';
  }
  #cards {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    gap: 40px;
    max-width: 840px;
  }

  #cards:hover > .card::after {
    opacity: 1;
  }

  .card {
    background-color: rgba(255, 255, 255, 0.1);
    border-radius: 10px;
    display: flex;
    height: 360px;
    flex-direction: column;
    position: relative;
    width: 360px;
  }

  .card:hover::before {
    opacity: 1;
  }

  .card::before,
  .card::after {
    border-radius: inherit;
    content: '';
    height: 100%;
    left: 0px;
    opacity: 0;
    position: absolute;
    top: 0px;
    transition: opacity 500ms;
    width: 100%;
  }

  .card::before {
    background: radial-gradient(
      800px circle at var(--mouse-x) var(--mouse-y),
      #48348b32,
      transparent 40%
    );
    z-index: 3;
  }

  .card::after {
    background: radial-gradient(
      600px circle at var(--mouse-x) var(--mouse-y),
      #48348b,
      transparent 40%
    );
    z-index: 1;
  }

  .card > .card-content {
    background-color: #161618;
    border-radius: inherit;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    flex-grow: 1;
    inset: 1px;
    padding: 16px;
    position: absolute;
    z-index: 2;
  }

  .card .card-content svg {
    fill: #a4a4a4; /* or your default color */
    stroke: #a4a4a4; /* or your default color */
    transition:
      fill 0.3s,
      stroke 0.3s;
  }

  .card:hover .card-content svg {
    fill: #48348b;
    stroke: #48348b;
  }
}

footer {
  p,
  h2 {
    font-family: 'Hedvig Letters Serif';
  }
}

@media screen and (max-width: 640px) {
  .card {
    height: 300px;
    width: 300px;
  }
}
</style>
