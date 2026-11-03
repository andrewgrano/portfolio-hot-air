<script setup>
import { ref } from 'vue'
import { Swiper, SwiperSlide } from 'swiper/vue'
import 'swiper/css'
import VideoModal from './VideoModal.vue'

const projects = [
  {
    id: 'designbase',
    title: 'Designbase',
    role: 'Development',
    href: 'https://designbase.com/',
    image: '/portfolio/designbase.png',
    alt: 'Screenshot of the Designbase desktop app',
    paragraphs: [
      'Andrew is a founding engineer at Designbase, an AI-native workspace for design systems, production code, and agents. Teams import a React component library, prototype from real product code, and share the same product context with designers, engineers, and agents.',
      'He built the Electron desktop app, turning product concepts into the workflows people use, and designs reusable React components for the product’s design system.',
    ],
  },
  {
    id: 'ycode',
    title: 'Ycode',
    role: 'Development',
    href: 'https://www.ycode.com/',
    image: '/portfolio/ycode.png',
    alt: 'Screenshot of the Ycode editor',
    paragraphs: [
      'Andrew worked on the Ycode product team for 3+ years as the lead front-end developer. Ycode is a powerful no-code website builder.',
      "Creating custom features from scratch for both the UI of the platform and the code behind the website which it generated, this is some of Andrew's proudest work. Animations powered by GSAP, a box-shadow generator using Tailwind CSS, and a custom slider/carousel/lightbox using Swiper JS are some examples of Andrew's work.",
    ],
  },
  {
    id: 'timescroll',
    title: 'TimeScroll Studio',
    role: 'Design + Development',
    href: 'https://timescroll.studio/',
    image: '/portfolio/timescroll.png',
    alt: 'Screenshot of TimeScroll Studio',
    paragraphs: [
      'TimeScroll studio allows users to scroll through time in their browser and experience the real distance between events. Create, explore, and share beautiful timelines that make history and stories visual and interactive.',
      'This full-stack web application was created solely by Andrew, primarily using AI development tools and Supabase as the back end.',
    ],
  },
  {
    id: 'dod',
    title: 'DoD OCR App',
    role: 'Design + Development',
    video: '/cbsuite-demo-video.mov',
    image: '/portfolio/dod.png',
    alt: 'Screenshot of DoD OCR App',
    paragraphs: [
      'Andrew designed and developed the front-end of this web app for the US Department of Defense while working as an official government contractor. It performs optical character recognition via file upload and download features.',
      'The web app is built with Typescript, React, Tanstack Table, Tailwind CSS, and Vite. Figma and LucidChart were used for designing the UI/UX.',
    ],
  },
  {
    id: 'csun',
    title: 'CSUN Styleguide',
    role: 'Design + Development',
    href: 'https://metaphor-v2.netlify.app/documentation/',
    image: '/portfolio/csun.png',
    alt: 'Screenshot of CSUN Styleguide',
    paragraphs: [
      'A custom style guide for Cal State University Northridge, built as an NPM package on top of bootstrap, designed and developed by Andrew.',
      'Featuring common reusable components and visuals tailored to the University, this style guide was used in multiple digital products for the campus.',
    ],
  },
  {
    id: 'feetures',
    title: 'feetures',
    role: 'Development',
    href: 'https://feetures.com/',
    image: '/portfolio/feetures.png',
    alt: 'Screenshot of Feetures website',
    paragraphs: [
      'A shopify website built from scratch by Andrew while working for Netalico - using Liquid, Javascript, and Scss.',
      'The site is completely custom and includes nearly every imaginable feature that an e-commerce website could have for both users and admins.',
    ],
  },
  {
    id: 'roaming',
    title: 'Roaming Love',
    role: 'Design + Development',
    href: 'https://www.roaminglove.com/',
    image: '/portfolio/roaming-love.png',
    alt: 'Screenshot of Roaming Love blog - Homepage',
    paragraphs: [
      'A community travel blog with hundreds of articles and authors. Built, designed, and maintained solely by Andrew.',
      'Hosted on Netlify, a static site generator powered the front end while Github hooks powered a CI/CD pipeline with WordPress as the backend.',
    ],
  },
  /*
  {
    id: 'landing',
    title: 'Landing Pages',
    role: 'Design + Development',
    slides: [
      { image: '/screenshot-infopacked.jpg', title: 'InfoPacked', url: 'https://infopacked.ycode.site/' },
      { image: '/screenshot-pbcottages.jpg', title: 'PB Cottages', url: 'https://pacificbeachcottages.com/' },
      { image: '/screenshot-wedding.jpg', title: 'My Wedding Website', url: 'https://andrewsigourneewedding.netlify.app/' },
      { image: '/screenshot-mediakit.jpg', title: 'Roaming Love Media Kit', url: 'http://mediakit.roaminglove.com/' },
      { image: '/screenshot-pdc.jpg', title: 'Picture Day Company', url: 'https://preview-pdc.ycode.site/' },
    ],
    paragraphs: [
      'Andrew has built a variety of custom Landing Pages throughout the years using a variety of technologies. He always strives to build creative, unique, accessible sites with semantic markup and responsive design.',
      'Click each slide to see the full landing page.',
    ],
  },
  */
]

const videoOpen = ref(false)
const landingSwiper = ref(null)
const landingIndex = ref(0)

function onLandingSwiper(instance) {
  landingSwiper.value = instance
}

function onLandingChange(instance) {
  landingIndex.value = instance.realIndex
}

function landingPrev() {
  landingSwiper.value?.slidePrev()
}

function landingNext() {
  landingSwiper.value?.slideNext()
}

function landingGo(index) {
  landingSwiper.value?.slideToLoop(index)
}
</script>

<template>
  <section class="portfolio" aria-label="Selected work">
    <div class="portfolio-inner">
      <article v-for="project in projects" :key="project.id" class="card">
        <a
          v-if="project.href || project.slides"
          class="card-stretch"
          :href="project.href || project.slides[landingIndex].url"
          target="_blank"
          rel="noopener noreferrer"
          :aria-label="project.slides ? `${project.title}: ${project.slides[landingIndex].title}` : undefined"
          :aria-labelledby="project.slides ? undefined : `project-${project.id}`"
        ></a>
        <button
          v-else-if="project.video"
          type="button"
          class="card-stretch"
          :aria-label="`Play ${project.title} demo`"
          @click="videoOpen = true"
        ></button>

        <div class="media">
          <div v-if="project.slides" class="media-fill slides">
            <swiper
              :slides-per-view="1"
              :loop="true"
              class="swiper"
              @swiper="onLandingSwiper"
              @slide-change="onLandingChange"
            >
              <swiper-slide v-for="slide in project.slides" :key="slide.url">
                <img :src="slide.image" :alt="slide.title">
              </swiper-slide>
            </swiper>
            <div class="slide-controls">
              <button type="button" aria-label="Previous slide" @click="landingPrev">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true">
                  <path d="M15 18L9 12L15 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              </button>
              <div class="dots">
                <button
                  v-for="(slide, index) in project.slides"
                  :key="slide.url"
                  type="button"
                  :class="{ active: landingIndex === index }"
                  :aria-label="`Go to ${slide.title}`"
                  @click="landingGo(index)"
                ></button>
              </div>
              <button type="button" aria-label="Next slide" @click="landingNext">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true">
                  <path d="M9 18L15 12L9 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              </button>
            </div>
          </div>

          <div v-else class="media-fill">
            <img :src="project.image" :alt="project.alt">
          </div>
        </div>

        <div class="caption">
          <div class="identity">
            <h2 :id="`project-${project.id}`" class="title">{{ project.title }}</h2>
            <p class="role">{{ project.role }}</p>
          </div>
          <div class="copy">
            <p v-for="paragraph in project.paragraphs" :key="paragraph">{{ paragraph }}</p>
          </div>
        </div>
      </article>
    </div>

    <VideoModal
      :is-open="videoOpen"
      video-src="/cbsuite-demo-video.mov"
      title="DoD OCR App Demo"
      @close="videoOpen = false"
    />
  </section>
</template>

<style scoped>
.portfolio {
  background: #F5F2EA;
  width: calc(100% + 60px);
  margin-left: -30px;
  margin-right: -30px;
  padding: 0 24px 72px;
}

.portfolio-inner {
  display: grid;
  grid-template-columns: 1fr;
  gap: 48px 24px;
  max-width: 1200px;
  margin: 0 auto;
}

.card {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 16px;
  min-width: 0;
  padding: 16px;
  background: #eeebe3;
  border: 1px solid #dedcd2;
  border-radius: 3px;
  cursor: pointer;
}

.card-stretch {
  position: absolute;
  inset: 0;
  z-index: 1;
  border: 0;
  padding: 0;
  background: transparent;
  cursor: pointer;
}

.card-stretch:focus-visible {
  outline: 2px solid #233e38;
  outline-offset: 2px;
}

.media {
  position: relative;
  aspect-ratio: 1904 / 967;
  overflow: hidden;
}

.media-fill {
  position: absolute;
  inset: 0;
  display: block;
  width: 100%;
  height: 100%;
}

.media img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top center;
  display: block;
}

.slides .swiper,
.slides :deep(.swiper-wrapper),
.slides :deep(.swiper-slide),
.slides :deep(.swiper-slide a) {
  height: 100%;
}

.slide-controls {
  position: absolute;
  left: 10px;
  right: 10px;
  bottom: 10px;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding: 6px 8px;
  background: rgba(245, 242, 234, 0.88);
  border-radius: 999px;
}

.slide-controls button {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2px;
  border: 0;
  background: none;
  color: #233e38;
  cursor: pointer;
}

.dots {
  display: flex;
  gap: 6px;
}

.dots button {
  width: 7px;
  height: 7px;
  padding: 0;
  border-radius: 50%;
  background: rgba(35, 62, 56, 0.28);
}

.dots button.active {
  background: #233e38;
}

.caption {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.identity {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.title {
  margin: 0;
  font-family: "Cormorant Garamond", Georgia, serif;
  font-weight: 400;
  font-size: 32px;
  line-height: 1.05;
  color: #233e38;
}

.role {
  margin: 0;
  font-family: "Instrument Sans", sans-serif;
  font-size: 13px;
  line-height: 1.5;
  color: #6d7a70;
}

.copy {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.copy p {
  margin: 0;
  font-family: "Instrument Sans", sans-serif;
  font-weight: 400;
  font-size: 14px;
  line-height: 1.5;
  color: #233e38;
}

@media (min-width: 700px) {
  .portfolio {
    padding: 0 max(48px, min(120px, 8.333vw)) 88px;
  }

  .portfolio-inner {
    grid-template-columns: 1fr 1fr;
  }
}

/* Three-up layout, kept for comparison.
@media (min-width: 1100px) {
  .portfolio-inner {
    grid-template-columns: 1fr 1fr 1fr;
  }
}
*/
</style>
