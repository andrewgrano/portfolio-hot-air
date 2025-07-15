<script setup>
import { ref, onMounted, onUnmounted, watch } from 'vue'

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  images: {
    type: Array,
    required: true
  },
  title: {
    type: String,
    default: ''
  }
})

const emit = defineEmits(['close'])

const currentImageIndex = ref(0)

const closeModal = () => {
  console.log('closeModal called')
  emit('close')
}

const nextImage = () => {
  currentImageIndex.value = (currentImageIndex.value + 1) % props.images.length
}

const prevImage = () => {
  currentImageIndex.value = currentImageIndex.value === 0 
    ? props.images.length - 1 
    : currentImageIndex.value - 1
}

const handleKeydown = (event) => {
  if (event.key === 'Escape') {
    closeModal()
  } else if (event.key === 'ArrowRight') {
    nextImage()
  } else if (event.key === 'ArrowLeft') {
    prevImage()
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
        <div class="flex items-center justify-between p-6 border-b border-gray-200">
          <h3 class="text-2xl font-bold text-[#2D2D2D]">{{ title }}</h3>
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
        
        <!-- Image Container -->
        <div class="relative">
          <!-- Image -->
          <img 
            :src="images[currentImageIndex]"
            :alt="`${title} screenshot ${currentImageIndex + 1}`"
            class="w-full h-auto max-h-[70vh] object-contain"
          >
        </div>
        
        <!-- Navigation Row -->
        <div class="flex items-center justify-center space-x-4 p-4">
          <button 
            @click="prevImage"
            class="swiper-button-prev-custom"
            aria-label="Previous image"
          >
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M15 18L9 12L15 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </button>
          
          <div class="swiper-pagination-custom justify-center">
            <button
              v-for="(image, index) in images"
              :key="index"
              @click="currentImageIndex = index"
              :class="[
                'swiper-pagination-bullet',
                currentImageIndex === index 
                  ? 'swiper-pagination-bullet-active' 
                  : ''
              ]"
              :aria-label="`Go to image ${index + 1}`"
            ></button>
          </div>
          
          <button 
            @click="nextImage"
            class="swiper-button-next-custom"
            aria-label="Next image"
          >
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M9 18L15 12L9 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </button>
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

.swiper-button-prev-custom,
.swiper-button-next-custom {
  color: #F5C15A;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
  border-radius: 4px;
  transition: all 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.swiper-button-prev-custom:hover,
.swiper-button-next-custom:hover {
  background-color: rgba(245, 193, 90, 0.1);
}

.swiper-pagination-custom {
  display: flex;
  gap: 8px;
  align-items: center;
}

.swiper-pagination-bullet {
  width: 8px;
  height: 8px;
  background: #D1D5DB;
  border-radius: 50%;
  opacity: 1;
  cursor: pointer;
  transition: all 0.2s ease;
  border: none;
  padding: 0;
}

.swiper-pagination-bullet-active {
  background: #F5C15A;
  transform: scale(1.2);
}
</style> 