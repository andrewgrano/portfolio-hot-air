<script setup>
import { ref } from 'vue'
</script>

<template>
  <a class="dont-animate col-span-1 sm:col-span-2 md:col-span-3 lg:col-span-6 bg-white border-2 border-[#F5C15A] rounded-[20px] p-8 flex flex-col hover:bg-[#2D2D2D] hover:text-white transition-all duration-150 cursor-pointer" target="timescrollstudio" href="https://timescroll.studio/">
    <div>
      <h4 class="text-[40px] font-bold tracking-[-0.03rem] mb-0 leading-none">TimeScroll Studio</h4>
      <p class="font-['Permanent_Marker'] text-[16px] text-[#F5C15A] mb-6">DESIGN + DEVELOPMENT</p>
      <img 
        src="/screenshot-timescroll.png"
        alt="Screenshot of TimeScroll Studio"
        class="mb-6"
      >
     
      <p class="text-[18px] mb-4 leading-tight">
        TimeScroll studio allows users to scroll through time in their browser and experience the real distance between events. Create, explore, and share beautiful timelines that make history and stories visual and interactive.
      </p>
      <p class="text-[18px] mb-4 leading-tight">
        This full-stack web application was created solely by Andrew, primarily using AI development tools and Supabase as the back end.
      </p>
    </div>
  </a>
</template>

<style scoped>
</style> 