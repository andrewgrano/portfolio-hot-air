<script setup>
import { ref } from 'vue'
import VideoModal from '../VideoModal.vue'

const isModalOpen = ref(false)

const openModal = () => {
  isModalOpen.value = true
}

const closeModal = () => {
  isModalOpen.value = false
}
</script>

<template>
  <div 
    class="dont-animate col-span-1 sm:col-span-2 md:col-span-3 lg:col-span-6 bg-white border-2 border-[#F5C15A] rounded-[20px] p-8 flex flex-col cursor-pointer hover:shadow-lg transition-shadow  hover:bg-[#2D2D2D] hover:text-white transition-all duration-150 cursor-pointer"
    @click="openModal"
  >
    <div>
      <h4 class="text-[40px] font-bold tracking-[-0.03rem] mb-0 leading-none">CB Suite</h4>
      <p class="font-['Permanent_Marker'] text-[16px] text-[#F5C15A] mb-6">DESIGN + DEVELOPMENT</p>
      <img 
        src="/screenshot-cbsuite.png"
        alt="Screenshot of CB Suite"
        class="mb-6"
      >
      <p class="text-[18px] mb-4 leading-tight">
        Andrew designed and developed the front-end of this HR software for the U.S. Navy while working as an official government contractor for Pantheon Data.
      </p>
      <p class="text-[18px] leading-tight">
        It is built with Typescript, React, Tanstack Table, Tailwind CSS, and Vite.  Figma and LucidChart were used for designing the UI/UX.  
      </p>
    </div>
  </div>
  
  <VideoModal
    :is-open="isModalOpen"
    video-src="/cbsuite-demo-video.mov"
    title="CB Suite Demo"
    @close="closeModal"
  />
</template>

<style scoped>
</style> 