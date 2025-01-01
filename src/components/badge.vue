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
      'from-[#3ED294] to-[#66EBB3]': color === 'green',
      'from-[#37CFCF] to-[#A1F6F6]': color === 'blue',
      'from-[#D19E3B] to-[#E9BE6A]': color === 'yellow',
      'bg-gradient-to-r': !first,
      'bg-gradient-to-l': first,
    }"
    class="text-[20px] sm:text-[18px] md:text-[19px] lg:text-[22px] rounded-[4px] inline-flex px-[10px] py-[5px]"
  >
    {{ text }}
  </div>
</template>

<style scoped>

</style>
