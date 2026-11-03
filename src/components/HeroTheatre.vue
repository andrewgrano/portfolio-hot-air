<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'
import { gsap } from 'gsap'

import cloud02 from '../assets/hero/cloud-02.svg'
import cloud03 from '../assets/hero/cloud-03.svg'
import cloud06 from '../assets/hero/cloud-06.svg'
import cloud08 from '../assets/hero/cloud-08.svg'
import balloonSmall from '../assets/hero/balloon-small.svg'
import balloonMedium from '../assets/hero/balloon-medium.svg'
import balloonLarge from '../assets/hero/balloon-large.svg'
import flameSmall from '../assets/hero/flame-small.svg'
import flameMedium from '../assets/hero/flame-medium.svg'
import flameLarge from '../assets/hero/flame-large.svg'

const STAGE_W = 1440
const STAGE_H = 689

const clouds = [
  { id: 'bank', src: cloud02, x: 560, y: -220, w: 940, h: 573.4, speed: 14, weave: false, front: false },
  { id: 'summits', src: cloud03, x: -40, y: 120, w: 740, h: 451.4, speed: 18, weave: true, front: false },
  { id: 'shelf', src: cloud06, x: -40, y: -120, w: 580, h: 353.8, speed: 22, weave: true, front: true },
  { id: 'tuft', src: cloud08, x: 960, y: 280, w: 330, h: 201.3, speed: 28, weave: true, front: true },
  // Starts just off the right and sits in the lower sky, so it crosses
  // while the first four are still exiting left.
  { id: 'low', src: cloud08, x: 1568, y: 450, w: 330, h: 201.3, speed: 16, weave: true, front: false },
]

const balloons = [
  { src: balloonSmall, flame: flameSmall, x: 900, y: 65, w: 44, h: 60.104, lift: 7, duration: 3.6, delay: 0.4, tilt: 1.4 },
  { src: balloonMedium, flame: flameMedium, x: 120, y: 180, w: 80, h: 109.28, lift: 11, duration: 4.4, delay: 1.1, tilt: -1.6 },
  { src: balloonLarge, flame: flameLarge, x: 1140, y: 260, w: 155, h: 211.73, lift: 16, duration: 5.2, delay: 0, tilt: 1.1 },
]

const root = ref(null)
const stage = ref(null)
const ready = ref(false)
const scale = ref(1)

let resizeObserver
let motionQuery
const tweens = []

function layout() {
  if (!root.value) return
  scale.value = root.value.clientWidth / STAGE_W
}

function track(tween) {
  tweens.push(tween)
  return tween
}

function toggleDepth(el) {
  if (el.dataset.weave !== 'true') return
  el.classList.toggle('is-front')
}

function driftCloud(el) {
  const width = Number(el.dataset.width)
  const left = Number(el.dataset.x)
  const speed = Number(el.dataset.speed)
  const exitX = -(left + width)
  const enterX = STAGE_W - left

  track(gsap.fromTo(el, { x: 0 }, {
    x: exitX,
    duration: (left + width) / speed,
    ease: 'none',
    onComplete: () => {
      toggleDepth(el)
      track(gsap.fromTo(el, { x: enterX }, {
        x: exitX,
        duration: (STAGE_W + width) / speed,
        ease: 'none',
        repeat: -1,
        onRepeat: () => toggleDepth(el),
      }))
    },
  }))
}

function floatBalloon(el) {
  const lift = Number(el.dataset.lift)
  const duration = Number(el.dataset.duration)
  const delay = Number(el.dataset.delay)
  const tilt = Number(el.dataset.tilt)
  const flame = el.querySelector('[data-flame]')
  const tiltEl = el.querySelector('[data-tilt]')

  const rise = duration * 0.46
  const fall = duration * 0.54
  const cycle = gsap.timeline({ repeat: -1, delay })
  cycle
    .to(el, { y: -lift, duration: rise, ease: 'sine.inOut' }, 0)
    .to(flame, { opacity: 1, duration: 0.35, ease: 'power1.out' }, 0.08)
    .to(flame, { opacity: 0, duration: 0.4, ease: 'power1.in' }, rise * 0.72)
    .to(el, { y: 0, duration: fall, ease: 'sine.inOut' })
  track(cycle)

  track(gsap.to(tiltEl, {
    rotation: tilt,
    duration: duration * 1.35,
    ease: 'sine.inOut',
    yoyo: true,
    repeat: -1,
    delay,
  }))
}

function play() {
  const cloudEls = stage.value.querySelectorAll('[data-cloud]')
  const balloonEls = stage.value.querySelectorAll('[data-balloon]')
  const nameEl = stage.value.querySelector('[data-name]')
  const roleEl = stage.value.querySelector('[data-role]')
  const reduce = window.matchMedia('(prefers-reduced-motion: reduce)').matches

  if (reduce) {
    gsap.set(cloudEls, { opacity: 1 })
    gsap.set(balloonEls, { opacity: 1, y: 0 })
    gsap.set([nameEl, roleEl], { opacity: 1, y: 0 })
    return
  }

  gsap.set(cloudEls, { opacity: 0 })
  gsap.set(balloonEls, { opacity: 0 })
  gsap.set(nameEl, { opacity: 0, y: 18 })
  gsap.set(roleEl, { opacity: 0, y: 10 })

  const intro = gsap.timeline()
  intro.to(cloudEls, { opacity: 1, duration: 1.35, ease: 'power2.out' }, 0)
  intro.to(balloonEls, { opacity: 1, duration: 1.05, ease: 'power2.out' }, 0.9)
  intro.to(nameEl, { opacity: 1, y: 0, duration: 1, ease: 'power2.out' }, 1.6)
  intro.to(roleEl, { opacity: 1, y: 0, duration: 0.85, ease: 'power2.out' }, 2.25)
  track(intro)

  cloudEls.forEach(driftCloud)
  balloonEls.forEach(floatBalloon)
}

onMounted(() => {
  layout()
  ready.value = true
  resizeObserver = new ResizeObserver(layout)
  resizeObserver.observe(root.value)
  play()

  motionQuery = window.matchMedia('(prefers-reduced-motion: reduce)')
  motionQuery.addEventListener('change', () => {
    tweens.splice(0).forEach((tween) => tween.kill())
    gsap.set(stage.value.querySelectorAll('[data-cloud], [data-balloon], [data-name], [data-role], [data-flame], [data-tilt]'), {
      clearProps: 'opacity,transform',
    })
    play()
  })
})

onBeforeUnmount(() => {
  resizeObserver?.disconnect()
  tweens.forEach((tween) => tween.kill())
})
</script>

<template>
  <section ref="root" class="hero" aria-label="Andrew Grano">
    <div ref="stage" class="stage" :class="{ ready }" :style="{ transform: `scale(${scale})` }">
      <div
        v-for="cloud in clouds"
        :key="cloud.id"
        class="cloud"
        :class="{ 'is-front': cloud.front }"
        data-cloud
        :data-x="cloud.x"
        :data-width="cloud.w"
        :data-speed="cloud.speed"
        :data-weave="cloud.weave ? 'true' : 'false'"
        :style="{
          left: `${cloud.x}px`,
          top: `${cloud.y}px`,
          width: `${cloud.w}px`,
          height: `${cloud.h}px`,
          '--cloud': `url('${cloud.src}')`,
        }"
      >
        <div class="blocker"></div>
        <img class="cloud-img" :src="cloud.src" :width="cloud.w" :height="cloud.h" alt="">
      </div>

      <div
        v-for="balloon in balloons"
        :key="balloon.src"
        class="floater"
        data-balloon
        :data-lift="balloon.lift"
        :data-duration="balloon.duration"
        :data-delay="balloon.delay"
        :data-tilt="balloon.tilt"
        :style="{ left: `${balloon.x}px`, top: `${balloon.y}px`, width: `${balloon.w}px`, height: `${balloon.h}px` }"
      >
        <div class="tilt" data-tilt>
          <img :src="balloon.src" :width="balloon.w" :height="balloon.h" alt="">
          <img class="flame" data-flame :src="balloon.flame" :width="balloon.w" :height="balloon.h" alt="">
        </div>
      </div>

      <h1 class="name" data-name>Andrew<br>Grano</h1>
      <p class="role" data-role>Front End Design Engineer</p>
    </div>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  overflow: hidden;
  background: #F5F2EA;
  aspect-ratio: 1440 / 689;
  width: calc(100% + 60px);
  margin-left: -30px;
  margin-right: -30px;
}

@media (min-width: 768px) {
  .hero {
    margin-top: -2rem;
  }
}

.stage {
  position: absolute;
  top: 0;
  left: 0;
  width: 1440px;
  height: 689px;
  transform-origin: top left;
  visibility: hidden;
}

.stage.ready {
  visibility: visible;
}

.cloud,
.floater {
  position: absolute;
  display: block;
  max-width: none;
}

.floater {
  z-index: 1;
}

.cloud {
  z-index: 0;
}

.cloud.is-front {
  z-index: 2;
}

.blocker {
  display: none;
  position: absolute;
  inset: 0;
  background: #F5F2EA;
  pointer-events: none;
  -webkit-mask-image: var(--cloud);
  -webkit-mask-repeat: no-repeat;
  -webkit-mask-size: 100% 100%;
  -webkit-mask-position: center;
  mask-image: var(--cloud);
  mask-repeat: no-repeat;
  mask-size: 100% 100%;
  mask-position: center;
  mask-mode: alpha;
}

.cloud.is-front .blocker {
  display: block;
}

.cloud-img {
  position: relative;
  display: block;
  max-width: none;
  opacity: 0.7;
}

.tilt {
  position: relative;
  width: 100%;
  height: 100%;
}

.tilt img {
  display: block;
  max-width: none;
}

.flame {
  position: absolute;
  left: 0;
  top: 0;
  opacity: 0;
}

.name,
.role {
  z-index: 3;
}

.name {
  position: absolute;
  left: 210px;
  top: 182px;
  width: 1020px;
  margin: 0;
  font-family: "Cormorant Garamond", Georgia, serif;
  font-weight: 400;
  font-size: 212px;
  line-height: 0.84;
  text-align: center;
  color: #233e38;
  text-shadow: 0 4px 24px rgba(255, 255, 255, 0.4);
}

.role {
  position: absolute;
  left: 470px;
  top: 588px;
  width: 500px;
  margin: 0;
  font-family: "Instrument Sans", sans-serif;
  font-weight: 400;
  font-size: 27px;
  line-height: 1.5;
  text-align: center;
  color: #6d7a70;
  text-shadow: 0 4px 24px rgba(255, 255, 255, 0.4);
}

@media (max-width: 767px) {
  .role {
    left: 0;
    top: 560px;
    width: 1440px;
    font-size: calc(24px / 100vw * 1440px);
    line-height: 1.15;
  }
}
</style>
