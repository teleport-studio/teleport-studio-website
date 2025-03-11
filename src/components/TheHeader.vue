<script setup lang="ts">
import { onMounted, ref, watch } from 'vue'
import { useRouter } from 'vue-router'
import { gsap } from 'gsap'

const router = useRouter()
const header = ref()

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
</script>

<template>
  <header
    ref="header"
    class="absolute z-50 top-4 lg:top-8 left-4 lg:left-8 right-4 lg:right-8 max-w-[2000px] mx-auto translate-y-[-150px] transition-all duration-500 overflow-hidden"
  >
    <div class="flex items-center gap-8">
      <img src="../assets/logo.png" alt="logo" class="h-8 w-8" />
      <div class="h-[1px] bg-black w-full"></div>
      <div class="flex justify-end w-[156px]">
        <button
          @click="router.push('/contact')"
          class="contact group relative inline-flex h-12 items-center justify-center overflow-hidden rounded-full border border-black bg-transparent font-medium cursor-pointer"
        >
          <div
            class="inline-flex w-full h-12 translate-y-0 items-center justify-center gap-2 px-6 text-black transition duration-500 group-hover:-translate-y-[150%]"
          >
            <span class="whitespace-nowrap">Let's work</span>
            <svg
              width="15"
              height="15"
              viewBox="0 0 15 15"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5"
            >
              <path
                d="M8.14645 3.14645C8.34171 2.95118 8.65829 2.95118 8.85355 3.14645L12.8536 7.14645C13.0488 7.34171 13.0488 7.65829 12.8536 7.85355L8.85355 11.8536C8.65829 12.0488 8.34171 12.0488 8.14645 11.8536C7.95118 11.6583 7.95118 11.3417 8.14645 11.1464L11.2929 8H2.5C2.22386 8 2 7.77614 2 7.5C2 7.22386 2.22386 7 2.5 7H11.2929L8.14645 3.85355C7.95118 3.65829 7.95118 3.34171 8.14645 3.14645Z"
                fill="currentColor"
                fill-rule="evenodd"
                clip-rule="evenodd"
              ></path>
            </svg>
          </div>
          <div
            class="absolute inline-flex h-12 w-full translate-y-[100%] items-center justify-center text-white transition duration-500 group-hover:translate-y-0"
          >
            <span
              class="absolute h-full w-full translate-y-full skew-y-12 scale-y-0 bg-black transition duration-500 group-hover:translate-y-0 group-hover:scale-150"
            ></span>
            <span class="z-10 flex items-center gap-2 text-nowrap">
              Let's work
              <svg
                width="15"
                height="15"
                viewBox="0 0 15 15"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5 text-white"
              >
                <path
                  d="M8.14645 3.14645C8.34171 2.95118 8.65829 2.95118 8.85355 3.14645L12.8536 7.14645C13.0488 7.34171 13.0488 7.65829 12.8536 7.85355L8.85355 11.8536C8.65829 12.0488 8.34171 12.0488 8.14645 11.8536C7.95118 11.6583 7.95118 11.3417 8.14645 11.1464L11.2929 8H2.5C2.22386 8 2 7.77614 2 7.5C2 7.22386 2.22386 7 2.5 7H11.2929L8.14645 3.85355C7.95118 3.65829 7.95118 3.34171 8.14645 3.14645Z"
                  fill="currentColor"
                  fill-rule="evenodd"
                  clip-rule="evenodd"
                ></path>
              </svg>
            </span>
          </div>
        </button>
      </div>
    </div>
  </header>
</template>

<style scoped>
.contact {
  font-family: 'Hedvig Letters Serif';
}
</style>
