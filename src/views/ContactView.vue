<script lang="ts" setup></script>
<template>
  <div class="flex md:items-center justify-center wrapper md:h-screen md:mt-0 mt-20">
    <div class="flex md:items-center w-full bg-[#161618]">
      <div
        class="flex flex-col items-start md:gap-24 gap-10 md:p-20 md:pb-0 p-6 pt-10 pb-0 max-w-[1580px] w-full mx-auto"
      >
        <div class="flex flex-col gap-4 md:text-nowrap">
          <h1 class="font-hedvig md:text-5xl text-3xl text-white">
            Have a idea?<br />Let's do it together.
          </h1>
          <p class="font-normal text-[#a4a4a4] md:text-base text-sm">
            Get in touch today and let's turn your idea into a remarkable success story!
          </p>
        </div>
        <div class="flex flex-col gap-2 md:gap-4 w-full">
          <div class="border-b border-[rgba(255,255,255,0.3)]">
            <a
              href="tel:+38670822681"
              class="flex md:items-center items-start flex-col md:flex-row md:justify-between gap-2 md:gap-0 text-white transition-colors duration-300 hover:text-[#48348B] md:py-4 py-2"
            >
              <h3 class="md:text-5xl text-3xl font-hedvig">Talk</h3>
              <p class="md:text-2xl text-base">+386 70 822 681</p>
            </a>
          </div>
          <div class="border-b border-[rgba(255,255,255,0.3)]">
            <a
              href="mailto:info@teleport-studio.com"
              class="flex md:items-center items-start flex-col md:flex-row md:justify-between gap-2 md:gap-0 text-white transition-colors duration-300 hover:text-[#48348B] md:py-4 py-2"
            >
              <h3 class="md:text-5xl text-3xl font-hedvig">Write</h3>
              <p class="md:text-2xl text-base">info@teleport-studio.com</p>
            </a>
          </div>
          <div class="border-b border-[rgba(255,255,255,0.3)]">
            <a
              href="https://www.instagram.com/teleport.agency?igsh=NjR5eWFqYXg5ZmF1"
              target="_blank"
              class="flex md:items-center items-start flex-col md:flex-row md:justify-between gap-2 md:gap-0 text-white transition-colors duration-300 hover:text-[#48348B] md:py-4 py-2"
            >
              <h3 class="md:text-5xl text-3xl font-hedvig">Dm us</h3>
              <p class="md:text-2xl text-base">Instagram</p>
            </a>
          </div>
        </div>
        <div
          class="flex flex-col pl-4 md:pb-24 pb-16 gap-2 border-l border-[rgba(255,255,255,0.5)] md:mt-10 mt-auto"
        >
          <h3 class="text-[#a4a4a4]">Follow us</h3>
          <a
            href="https://www.instagram.com/teleport.agency?igsh=NjR5eWFqYXg5ZmF1"
            target="_blank"
            class="flex items-center justify-between text-white transition-colors duration-300 hover:text-[#48348B]"
          >
            <p class="text-base font-hedvig">Instagram</p>
          </a>
          <a
            href="https://www.instagram.com/teleport.agency?igsh=NjR5eWFqYXg5ZmF1"
            target="_blank"
            class="flex items-center justify-between text-white transition-colors duration-300 hover:text-[#48348B]"
          >
            <p class="text-base font-hedvig">Tiktok</p>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.font-hedvig {
  font-family: 'Hedvig Letters Serif';
}
.wrapper {
  min-height: none;
}
@media screen and (max-width: 48rem) {
  .wrapper {
    min-height: calc(100dvh - 80px);
  }
}
</style>
