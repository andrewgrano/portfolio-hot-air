<script setup>
import { ref, onMounted } from 'vue'

// Initialize Swiper or other image gallery functionality if needed
</script>

<template>
  <a class="col-span-1 sm:col-span-2 md:col-span-3 lg:col-span-8 bg-white border-2 border-[#F5C15A] rounded-[20px] p-8 pb-0 flex flex-col justify-between overflow-hidden hover:bg-[#2D2D2D] hover:text-white transition-all duration-150 cursor-pointer" target="ycode" href="https://www.ycode.com/">
    <div class="flex flex-col lg:flex-row gap-10 mb-10">
      <div>
        <h4 class="text-[40px] font-bold tracking-[-0.03rem] mb-0 leading-none">Ycode</h4>
        <p class="font-['Permanent_Marker'] text-[16px] text-[#F5C15A] mb-6">DEVELOPMENT</p>
      </div>
      <div>
        <p class="text-[18px] mb-4 leading-tight">
          Andrew worked on the Ycode product team for 3+ years as the lead front-end developer. Ycode is a powerful no-code website builder.
        </p>
        <p class="text-[18px] leading-tight">
          Creating custom features from scratch for both the UI of the platform and the code behind the website which it generated, this is some of Andrew's proudest work. Animations powered by GSAP, a box-shadow generator using Tailwind CSS, and a custom slider/carousel/lightbox using Swiper JS are some examples of the Andrew's work.
        </p>
      </div>
    </div>
    <div class="flex justify-between mb-[-8px]">
      <img 
        src="/screenshot-ycode-1.png"
        alt="Screenshot of Ycode platform - animation interface"
        class="w-1/3"
      >
      <img 
        src="/screenshot-ycode-2.png"
        alt="Screenshot of Ycode platform - slider interface"
        class="w-1/3"
      >
      <img 
        src="/screenshot-ycode-3.png"
        alt="Screenshot of Ycode platform - box shadow interface"
        class="w-1/3"
      >
    </div>
  </a>
</template>

<style scoped>
</style> 