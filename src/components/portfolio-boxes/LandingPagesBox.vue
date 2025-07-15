<script setup>
import { ref, onMounted, computed } from 'vue'
import { Swiper, SwiperSlide } from 'swiper/vue'
import { Navigation, Pagination } from 'swiper/modules'
import 'swiper/css'
import 'swiper/css/navigation'
import 'swiper/css/pagination'

const slides = ref([
  {
    image: '/screenshot-infopacked.jpg',
    title: 'InfoPacked',
    url: 'https://infopacked.ycode.site/'
  },
  {
    image: '/screenshot-pbcottages.jpg',
    title: 'PB Cottages',
    url: 'https://pacificbeachcottages.com/'
  },
  {
    image: '/screenshot-wedding.jpg',
    title: 'My Wedding Website',
    url: 'https://andrewsigourneewedding.netlify.app/'
  },
  {
    image: '/screenshot-mediakit.jpg',
    title: 'Roaming Love Media Kit',
    url: 'http://mediakit.roaminglove.com/'
  },
  {
    image: '/screenshot-pdc.jpg',
    title: 'Picture Day Company',
    url: 'https://preview-pdc.ycode.site/'
  },
  // Add more landing pages as needed
])

const swiperRef = ref(null)
const currentSlide = ref(0)

const goToSlide = (index) => {
  console.log('goToSlide called with index:', index)
  console.log('swiperRef.value:', swiperRef.value)
  
  if (swiperRef.value) {
    console.log('swiperRef.value.swiper:', swiperRef.value.swiper)
    console.log('swiperRef.value.$el:', swiperRef.value.$el)
    
    // Try different ways to access the swiper instance
    if (swiperRef.value.swiper) {
      swiperRef.value.swiper.slideTo(index)
    } else if (swiperRef.value.$el && swiperRef.value.$el.swiper) {
      swiperRef.value.$el.swiper.slideTo(index)
    } else {
      console.log('Could not find swiper instance')
    }
  }
}

const goToPrev = () => {
  console.log('goToPrev called')
  console.log('swiperRef.value:', swiperRef.value)
  
  if (swiperRef.value) {
    if (swiperRef.value.swiper) {
      swiperRef.value.swiper.slidePrev()
    } else if (swiperRef.value.$el && swiperRef.value.$el.swiper) {
      swiperRef.value.$el.swiper.slidePrev()
    }
  }
}

const goToNext = () => {
  console.log('goToNext called')
  console.log('swiperRef.value:', swiperRef.value)
  
  if (swiperRef.value) {
    if (swiperRef.value.swiper) {
      swiperRef.value.swiper.slideNext()
    } else if (swiperRef.value.$el && swiperRef.value.$el.swiper) {
      swiperRef.value.$el.swiper.slideNext()
    }
  }
}

const onSlideChange = (swiper) => {
  console.log('Slide changed to:', swiper.activeIndex)
  currentSlide.value = swiper.realIndex
}

const onSwiperInit = (swiper) => {
  console.log('Swiper initialized:', swiper)
  console.log('swiperRef.value after init:', swiperRef.value)
}
</script>

<template>
  <div class="col-span-1 sm:col-span-2 md:col-span-3 lg:col-span-4 row-span-2 md:row-span-1 lg:row-span-2 bg-white border-2 border-[#F5C15A] rounded-[20px] p-8 flex flex-col  hover:bg-[#2D2D2D] group hover:text-white transition-all duration-150 ">
    <h4 class="text-[40px] font-bold tracking-[-0.03rem] mb-2">Landing Pages</h4>
    <p class="font-['Permanent_Marker'] text-[16px] text-[#F5C15A] mb-6">DESIGN + DEVELOPMENT</p>
    
    <p class="text-[18px] mb-6 leading-tight">
      Andrew has built a variety of custom Landing Pages throughout the years using a variety of technologies. He always strives to build creative, unique, accessible sites with semantic markup and responsive design.
    </p>

    <div class="flex flex-col">
      <div class="mb-4">
        <swiper
          ref="swiperRef"
          :modules="[Navigation, Pagination]"
          :slides-per-view="1"
          :space-between="30"
          :loop="true"
          @slide-change="onSlideChange"
          @swiper="onSwiperInit"
          class="swiper-below-controls rounded-lg overflow-hidden shadow-[3px_4px_4px_0px_rgba(0,0,0,0.25)]"
        >
          <swiper-slide v-for="(slide, index) in slides" :key="index">
            <a :href="slide.url" target="_blank" class="block h-full">
              <img 
                :src="slide.image"
                :alt="slide.title"
                class="w-full h-auto"
              >
            </a>
          </swiper-slide>
        </swiper>
      </div>
      
      <!-- Custom navigation row -->
      <div class="flex items-center justify-center space-x-4">
        <button 
          @click="goToPrev"
          class="swiper-button-prev-custom"
          aria-label="Previous slide"
        >
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M15 18L9 12L15 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </button>
        
        <div class="swiper-pagination-custom justify-center">
          <button
            v-for="(slide, index) in slides"
            :key="index"
            @click="goToSlide(index)"
            :class="[
              'swiper-pagination-bullet',
              { 'swiper-pagination-bullet-active': currentSlide === index }
            ]"
            :aria-label="`Go to slide ${index + 1}`"
          ></button>
        </div>
        
        <button 
          @click="goToNext"
          class="swiper-button-next-custom"
          aria-label="Next slide"
        >
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M9 18L15 12L9 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </button>
      </div>
    </div>

    <p class="text-[16px] text-[#686868] mt-4 text-center group-hover:text-white">
      Click each slide to see the full landing page
    </p>
  </div>
</template>

<style scoped>
.swiper-below-controls {
  --swiper-navigation-size: 24px;
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

:deep(.swiper-wrapper) {
  margin-bottom: 0;
}

:deep(.swiper-slide) {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style> 