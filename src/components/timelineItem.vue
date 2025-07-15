<script setup>
import { ref, computed, onMounted } from 'vue'
import { gsap } from "gsap"
import { ScrollTrigger } from "gsap/ScrollTrigger"

gsap.registerPlugin(ScrollTrigger)

const props = defineProps({
  years: String,
  title: String,
  company: String,
  index: Number,
  isLast: Boolean,
  description: String,
})

const timelineItemRef = ref(null)

const isEven = (n) => { return n % 2 == 0; }

const itemIsEven = computed(() => {
  return isEven(props.index)
})

const isFirst = computed(() => {
  return props.index === 0
})

onMounted(() => {
  // Set initial state
  gsap.set(timelineItemRef.value, {
    opacity: 0,
    x: itemIsEven.value ? -50 : 50
  })

  // Create scroll trigger animation
  gsap.to(timelineItemRef.value, {
    opacity: 1,
    x: 0,
    duration: 0.8,
    ease: "power2.out",
    scrollTrigger: {
      trigger: timelineItemRef.value,
      start: "top 85%",
      end: "bottom 15%",
      toggleActions: "play none none reverse"
    }
  })
})
</script>

<template>
  <li class="flex items-center justify-center relative">
    <div class="absolute bg-[#F5C15A] rounded-full h-[20px] w-[20px] left-[-25px] sm:left-[initial]"  />
    <div 
      :class="{
        'top-[50%]': isFirst,
        'bottom-[50%]': isLast,
      }"
      class="absolute bg-[#F5C15A] h-[100%] w-[5px] left-[-17px] sm:left-[initial]" 
    />
    <div
      ref="timelineItemRef"
      :class="{
        // 'bg-[#BDD2E0] text-[#336182] border-[#4F94C5] ml-[30px] sm:mr-[350px] lg:mr-[480px]': itemIsEven,
        // 'bg-[#98DBB1] text-[#1A543C] border-[#4FC565] ml-[30px] sm:ml-[350px] lg:ml-[480px]': !itemIsEven,
        'ml-[30px] sm:mr-[350px] lg:mr-[480px]': itemIsEven,
        'ml-[30px] sm:ml-[350px] lg:ml-[480px]': !itemIsEven,
        'bg-white border-2 border-[#F5C15A] rounded-[20px] py-6 px-12': true,
        'sm:mt-[-25px]': !isFirst,
        'sm:mb-[-25px]': !isLast,
      }"
      class="rounded-[20px] w-[275px] lg:w-[400px] text-[20px] leading-tight px-[20px] py-[10px] mb-[25px] sm:mb-[-25px] border-2"
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
