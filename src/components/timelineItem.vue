<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  years: String,
  title: String,
  company: String,
  index: Number,
  isLast: Boolean,
  description: String,
})

const isEven = (n) => { return n % 2 == 0; }

const itemIsEven = computed(() => {
  return isEven(props.index)
})

const isFirst = computed(() => {
  return props.index === 0
})

</script>

<template>

  <li class="flex items-center justify-center relative">
    <div class="absolute bg-[#D09D3A] rounded-full h-[20px] w-[20px] left-[-25px] sm:left-[initial]"  />
    <div 
      :class="{
        'top-[50%]': isFirst,
        'bottom-[50%]': isLast,
      }"
      class="absolute bg-[#D09D3A] h-[100%] w-[5px] left-[-17px] sm:left-[initial]" 
    />
    <div 
      :class="{
        'from-[#37CFCF] to-[#A1F6F6] ml-[30px] sm:mr-[350px] lg:mr-[480px] bg-gradient-to-l': itemIsEven,
        'from-[#3ED294] to-[#66EBB3] ml-[30px] sm:ml-[350px] lg:ml-[480px] bg-gradient-to-r': !itemIsEven,
        'sm:mt-[-25px]': !isFirst,
        'sm:mb-[-25px]': !isLast,

      }"
      class="rounded-[4px] w-[275px] lg:w-[400px] text-[20px] leading-tight px-[20px] py-[10px] mb-[25px] sm:mb-[-25px]"
    >
      <div class="font-bold">{{ years }}</div>
      <div class="font-bold">{{ title }}</div>
      <div class="">{{ company }}</div>
      <p class="my-[10px] text-[16px] opacity-[90%]"> 
        {{ description }}
      </p>
    </div>
  </li>

</template>

<style scoped>
</style>
