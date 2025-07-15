<script setup>
import CSUNBox from './portfolio-boxes/CSUNBox.vue'
import YcodeBox from './portfolio-boxes/YcodeBox.vue'
import RoamingLoveBox from './portfolio-boxes/RoamingLoveBox.vue'
import LandingPagesBox from './portfolio-boxes/LandingPagesBox.vue'
import FeeturesBox from './portfolio-boxes/FeeturesBox.vue'
import TimeScrollBox from './portfolio-boxes/TimeScrollBox.vue'
import CBSuiteBox from './portfolio-boxes/CBSuiteBox.vue'
import { ref, onMounted, nextTick } from 'vue'
import { gsap } from "gsap"
import { ScrollTrigger } from "gsap/ScrollTrigger"

gsap.registerPlugin(ScrollTrigger)

onMounted(async () => {
  await nextTick()
  
  // Target all portfolio box elements - both anchor tags and divs
  // let cards = document.querySelectorAll('.bento-portfolio-section a[target], .bento-portfolio-section .col-span-6, .bento-portfolio-section .col-span-4')
  
  // If that doesn't work, try a broader selector
  // if (cards.length < 7) {
    // cards = document.querySelectorAll('a[target], .col-span-6, .col-span-4')
  // }
  
  // // If still not enough, try targeting grid items
  // if (cards.length < 7) {
    // cards = document.querySelectorAll('.bento-portfolio-section .grid > *')
  // }
  let cards = document.querySelectorAll('.bento-portfolio-section .grid > *:not(.dont-animate)')
  
  console.log('Found cards:', cards.length)
  
  if (cards.length > 0) {
    // Set initial state for all cards
    gsap.set(cards, {
      opacity: 0,
      y: 50,
      immediateRender: true
    })
    
    // Create individual ScrollTriggers for each card
    cards.forEach((card, index) => {
      gsap.to(card, {
        opacity: 1,
        y: 0,
        duration: 0.8,
        ease: "power2.out",
        scrollTrigger: {
          trigger: card,
          start: "top 85%",
          end: "bottom 15%",
          toggleActions: "play none none reverse"
        }
      })
    })
  }
})
</script>

<template>
  <section class="bento-portfolio-section mb-[125px] mt-[30px] lg:mt-[100px]">
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-6 lg:grid-cols-12 gap-4 sm:gap-4 md:gap-6">
      <TimeScrollBox/>
      <CBSuiteBox />
      <CSUNBox />
      <LandingPagesBox class="hidden md:flex lg:hidden" />
      <YcodeBox />
      <FeeturesBox  />
      <LandingPagesBox class="flex md:hidden lg:flex" />
      <RoamingLoveBox />
    </div>
  </section>
</template>

<style scoped>
</style> 