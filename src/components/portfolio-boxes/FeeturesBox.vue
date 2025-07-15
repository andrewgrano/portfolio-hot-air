<script setup>
import { ref } from 'vue'

const bulletPoints = ref([
  'Product listing page with carousels, video player, stylized details, reviews, etc',
  'Product cards that swap images and display sizes, colors, and stock',
  'Filterable product list powered by Vue.JS',
  'Nearly everything can be updated by the shop owners with no-code',
])
</script>

<template>
  <a class="col-span-0 sm:col-span-2 md:col-span-3 lg:col-span-8 bg-white border-2 border-[#F5C15A] rounded-[20px] p-8 flex flex-col hover:bg-[#2D2D2D] hover:text-white transition-all duration-150 cursor-pointer" target="feetures" href="https://feetures.com/">
    <div class="flex flex-col lg:flex-row gap-8 items-start">
      <div>
        <h4 class="text-[40px] font-bold tracking-[-0.03rem] mb-0 leading-none">feetures</h4>
        <p class="font-['Permanent_Marker'] text-[16px] text-[#F5C15A] mb-6">DEVELOPMENT</p>
      
        <p class="text-[18px] mb-4 leading-tight">
          A shopify website built from scratch by Andrew while working for Netalico - using Liquid, Javascript, and Scss.
        </p>

        <p class="text-[18px] mb-4 leading-tight">
          The site is completely custom and includes nearly every imaginable feature that an e-commerce website could have for both users and admins.
        </p>
      </div>
      <div>
        <img 
          src="/screenshot-feetures.png"
          alt="Screenshot of Feetures website"
          class="w-full lg:w-auto"
        >
      </div>
    </div> 
  </a>
</template>

<style scoped>
</style> 