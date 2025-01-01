<script setup>
import { ref } from 'vue'

defineProps({
  name: String,
  description: String,
  imgSrc: String,
  url: String,
})

</script>

<template>

  <li class="relative">
    <a :href="url" :target="name">
      <div class="group overflow-hidden rounded-lg border-solid border-[5px] border-[#eee] bg-gray-100 focus-within:ring-2 focus-within:ring-indigo-500 focus-within:ring-offset-2 focus-within:ring-offset-gray-100">
        <img :src="imgSrc" :alt="`Screenshot of  ${name} website`" class="pointer-events-none aspect-[10/7] object-cover group-hover:opacity-75">
      </div>
      <p class="pointer-events-none mt-2 block truncate font-medium text-gray-900">
        {{ name }}
      </p>
      <p class="pointer-events-none block text-sm font-medium text-gray-500">
        {{ description }}
      </p>
    </a>
  </li>

</template>

<style scoped>
</style>
