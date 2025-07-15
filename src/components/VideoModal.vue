<script setup>
import { ref, onMounted, onUnmounted, watch } from 'vue'

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  videoSrc: {
    type: String,
    required: true
  },
  title: {
    type: String,
    default: ''
  }
})

const emit = defineEmits(['close'])

const closeModal = () => {
  console.log('closeModal called')
  emit('close')
}

const handleKeydown = (event) => {
  if (event.key === 'Escape') {
    closeModal()
  }
}

// Watch for modal open/close to manage body scroll
watch(() => props.isOpen, (isOpen) => {
  if (isOpen) {
    document.body.style.overflow = 'hidden'
    document.addEventListener('keydown', handleKeydown)
  } else {
    document.body.style.overflow = 'auto'
    document.removeEventListener('keydown', handleKeydown)
  }
}, { immediate: true })

// Clean up on component unmount
onUnmounted(() => {
  document.body.style.overflow = 'auto'
  document.removeEventListener('keydown', handleKeydown)
})
</script>

<template>
  <Transition name="modal">
    <div v-if="isOpen" class="fixed inset-0 z-50 flex items-center justify-center">
      <!-- Backdrop -->
      <div 
        class="absolute inset-0 bg-black bg-opacity-75"
        @click="closeModal"
      ></div>
      
      <!-- Modal Content -->
      <div 
        class="relative bg-white rounded-[20px] max-w-4xl max-h-[90vh] overflow-hidden shadow-2xl z-10"
        @click.stop
      >
        <!-- Header -->
        <div class="flex items-center justify-between px-6 pt-4 ">
          <h3 class="text-3xl font-bold text-[#2D2D2D]">{{ title }}</h3>
          <button 
            @click="closeModal"
            class="text-gray-500 hover:text-gray-700 transition-colors p-2"
            aria-label="Close modal"
          >
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M18 6L6 18M6 6L18 18" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </button>
        </div>
        
        <!-- Video Container -->
        <div class="relative p-6">
          <video 
            :src="videoSrc"
            controls
            class="w-full h-auto max-h-[70vh] object-contain"
            preload="metadata"
          >
            Your browser does not support the video tag.
          </video>
        </div>
      </div>
    </div>
  </Transition>
</template>

<style scoped>
.modal-enter-active,
.modal-leave-active {
  transition: all 0.3s ease;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
  transform: scale(0.9);
}

.modal-enter-to,
.modal-leave-from {
  opacity: 1;
  transform: scale(1);
}
</style> 