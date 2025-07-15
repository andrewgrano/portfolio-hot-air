<script setup>
import { ref } from 'vue'
</script>

<template>
  <a class="col-span-1 sm:col-span-2 md:col-span-3 lg:col-span-8 bg-white border-2 border-[#F5C15A] rounded-[20px] p-8 flex flex-col hover:bg-[#2D2D2D] hover:text-white transition-all duration-150 cursor-pointer" target="roaminglove" href="https://www.roaminglove.com/">
    <div class="flex flex-col lg:flex-row gap-8">
      <div class="hidden lg:block">
        <img 
          src="/screenshot-roaming-love.png"
          alt="Screenshot of Roaming Love blog - Homepage"
          class="w-full lg:w-auto"
        >
      </div>
      <div>
        <h4 class="text-[40px] font-bold tracking-[-0.03rem] mb-0 leading-none">Roaming Love</h4>
        <p class="font-['Permanent_Marker'] text-[16px] text-[#F5C15A] mb-6">DESIGN + DEVELOPMENT</p>

        <div class="block lg:hidden mb-6">
          <img 
            src="/screenshot-roaming-love.png"
            alt="Screenshot of Roaming Love blog - Homepage"
            class="w-full lg:w-auto"
          >
        </div>
        
        <p class="text-[18px] mb-4 leading-tight">
          A community travel blog with hundreds of articles and authors. Built, designed, and maintained solely by Andrew.
        </p>
        <p class="text-[18px] leading-tight">
          Hosted on Netlify, a static site generator powered the front end while Github hooks powered a CI/CD pipeline with WordPress as the backend.
        </p>
      </div>
    </div>
  </a>
</template>

<style scoped>
</style> 