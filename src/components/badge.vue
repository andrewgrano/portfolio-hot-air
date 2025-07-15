<script setup>
import { ref } from 'vue'

defineProps({
  text: String,
  color: String,
  first: Boolean,
})

</script>

<template>
  <div 
    :class="{
      'bg-[#98DBB1] text-[#1A543C] border-[#4FC565]': color === 'green',
      'bg-[#BDD2E0] text-[#336182] border-[#4F94C5]': color === 'blue',
      'bg-[#F1D6A1] text-[#54411C] border-[#F5C15A]': color === 'yellow',
    }"
    class="text-[20px] sm:text-[18px] md:text-[19px] lg:text-[22px] rounded-[20px] inline-flex px-[16px] pt-[5px] pb-[3px] border-2 font-bold"
  >
    {{ text }}
  </div>
</template>

<style scoped>

</style>
