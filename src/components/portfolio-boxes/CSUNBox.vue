<script setup>
import { ref } from 'vue'
</script>

<template>
  <a class="col-span-1 sm:col-span-2 md:col-span-3 lg:col-span-4 bg-white border-2 border-[#F5C15A] rounded-[20px] p-8 flex flex-col hover:bg-[#2D2D2D] hover:text-white transition-all duration-150 cursor-pointer" target="metaphor" href="https://metaphor-v2.netlify.app/documentation/">
    <h4 class="text-[40px] font-bold tracking-[-0.03rem] mb-0 leading-none">CSUN Styleguide</h4>
    <p class="font-['Permanent_Marker'] text-[16px] text-[#F5C15A] mb-6">DESIGN + DEVELOPMENT</p>
    
    <img 
      src="/screenshot-csun-styleguide.png"
      alt="Screenshot of CSUN Styleguide"
      class="mb-6"
    >
    
    <p class="text-[18px] leading-tight mb-4">
      A custom style guide for Cal State University Northridge, built as an NPM package on top of bootstrap, designed and developed by Andrew.</p>
    <p class="text-[18px] leading-tight">
      Featuring common reusable components and visuals tailored to the University, this style guide was used in multiple digital products for the campus.    
    </p>
  </a>
</template>

<style scoped>
</style> 