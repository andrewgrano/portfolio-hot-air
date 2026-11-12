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
  // Sits further left so the small balloon can rise straight out of it.
  { id: 'tuft', src: cloud08, x: 912, y: 280, w: 330, h: 201.3, speed: 28, weave: true, front: true },
  // Starts just off the right and sits in the lower sky, so it crosses
  // while the first four are still exiting left.
  { id: 'low', src: cloud08, x: 1568, y: 450, w: 330, h: 201.3, speed: 16, weave: true, front: false },
]

const balloons = [
  // Rises straight up out of the tuft (cloud-08).
  { src: balloonSmall, flame: flameSmall, x: 900, y: 65, w: 44, h: 60.104, lift: 7, duration: 3.6, delay: 0.4, tilt: 1.4, riseSpeed: 52, riseDelay: 0.25, riseBehind: 'tuft' },
  { src: balloonMedium, flame: flameMedium, x: 120, y: 180, w: 80, h: 109.28, lift: 11, duration: 4.4, delay: 1.1, tilt: -1.6, riseSpeed: 78, riseDelay: 1.55 },
  { src: balloonLarge, flame: flameLarge, x: 1140, y: 260, w: 155, h: 211.73, lift: 16, duration: 5.2, delay: 0, tilt: 1.1, riseSpeed: 82, riseDelay: 0 },
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
  const flame = el.querySelector('[data-flame]')

  const rise = duration * 0.46
  const fall = duration * 0.54
  const cycle = gsap.timeline({ repeat: -1 })
  cycle
    .to(el, { y: -lift, duration: rise, ease: 'sine.inOut' }, 0)
    .to(flame, { opacity: 1, duration: 0.35, ease: 'power1.out' }, 0.08)
    .to(flame, { opacity: 0, duration: 0.4, ease: 'power1.in' }, rise * 0.72)
    .to(el, { y: 0, duration: fall, ease: 'sine.inOut' })
  track(cycle)
}

function riseBalloon(el) {
  const top = Number(el.dataset.y)
  const height = Number(el.dataset.height)
  const speed = Number(el.dataset.riseSpeed)
  let delay = Number(el.dataset.riseDelay)
  // Start below the hero, which sits a little past the stage.
  const clip = Math.max(STAGE_H, root.value.clientHeight / scale.value)
  let distance = clip - top + height + 16
  let holdUntilCovered = false

  const behindId = el.dataset.riseBehind
  if (behindId) {
    const cloud = clouds.find((item) => item.id === behindId)
    if (cloud) {
      // Wait until the drifting cloud covers this x, then climb straight up.
      const tuck = 62
      delay = Math.max(0, (cloud.x - (Number(el.dataset.x) - tuck)) / cloud.speed)
      distance = cloud.y + 105 - top
      holdUntilCovered = true
    }
  }

  const duration = distance / speed
  const flame = el.querySelector('[data-flame]')
  const tiltEl = el.querySelector('[data-tilt]')

  gsap.set(el, { y: distance, opacity: holdUntilCovered ? 0 : 1 })
  gsap.set(flame, { opacity: 0 })

  const rise = gsap.timeline({
    delay,
    onComplete: () => floatBalloon(el),
  })
  if (holdUntilCovered) rise.set(el, { opacity: 1 }, 0)
  rise
    .to(el, { y: 0, duration, ease: 'power1.out' }, 0)
    .to(flame, { opacity: 1, duration: 0.4, ease: 'power1.out' }, 0.15)
    .to(flame, { opacity: 0, duration: 0.45, ease: 'power1.in' }, Math.max(0.2, duration - 0.75))
  track(rise)

  track(gsap.to(tiltEl, {
    rotation: Number(el.dataset.tilt),
    duration: Number(el.dataset.duration) * 1.35,
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
    gsap.set(cloudEls, { opacity: 1, clearProps: 'filter' })
    gsap.set(balloonEls, { opacity: 1, y: 0 })
    gsap.set([nameEl, roleEl], { opacity: 1, y: 0, clearProps: 'filter' })
    return
  }

  gsap.set(cloudEls, { opacity: 0, filter: 'blur(18px)' })
  gsap.set(nameEl, { opacity: 0, y: 72, filter: 'blur(24px)' })
  gsap.set(roleEl, { opacity: 0, y: 40, filter: 'blur(10px)' })

  const intro = gsap.timeline()
  intro.to(cloudEls, {
    opacity: 1,
    filter: 'blur(0px)',
    duration: 1.35,
    ease: 'power2.out',
    onComplete: () => gsap.set(cloudEls, { clearProps: 'filter' }),
  }, 0)
  intro.to(nameEl, {
    opacity: 1,
    y: 0,
    filter: 'blur(0px)',
    duration: 1.8,
    ease: 'power3.out',
    onComplete: () => gsap.set(nameEl, { clearProps: 'filter' }),
  }, 1.45)
  intro.to(roleEl, {
    opacity: 1,
    y: 0,
    filter: 'blur(0px)',
    duration: 1.45,
    ease: 'power3.out',
    onComplete: () => gsap.set(roleEl, { clearProps: 'filter' }),
  }, 2.45)
  track(intro)

  cloudEls.forEach(driftCloud)
  balloonEls.forEach(riseBalloon)
}

onMounted(() => {
  layout()
  resizeObserver = new ResizeObserver(layout)
  resizeObserver.observe(root.value)
  play()
  ready.value = true

  motionQuery = window.matchMedia('(prefers-reduced-motion: reduce)')
  motionQuery.addEventListener('change', () => {
    tweens.splice(0).forEach((tween) => tween.kill())
    gsap.set(stage.value.querySelectorAll('[data-cloud], [data-balloon], [data-name], [data-role], [data-flame], [data-tilt]'), {
      clearProps: 'opacity,transform,filter',
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
        }"
      >
        <img class="cloud-img" :src="cloud.src" :width="cloud.w" :height="cloud.h" alt="">
      </div>

      <div
        v-for="balloon in balloons"
        :key="balloon.src"
        class="floater"
        data-balloon
        :data-x="balloon.x"
        :data-y="balloon.y"
        :data-height="balloon.h"
        :data-rise-behind="balloon.riseBehind"
        :data-lift="balloon.lift"
        :data-duration="balloon.duration"
        :data-delay="balloon.delay"
        :data-tilt="balloon.tilt"
        :data-rise-speed="balloon.riseSpeed"
        :data-rise-delay="balloon.riseDelay"
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
  container-type: inline-size;
  background-color: #F5F2EA;
  background-image: linear-gradient(
    170deg,
    #f7c4e2 0%,
    rgba(255, 154, 168, 0.82) 14%,
    rgba(255, 176, 138, 0.62) 30%,
    rgba(255, 206, 156, 0.32) 48%,
    rgba(255, 206, 156, 0) 68%
  );
  background-repeat: no-repeat;
  /* Sunset stays on the original scene. The hero is only a little taller. */
  background-size: 100% calc(100cqi * 689 / 1440);
  height: calc(100cqi * 689 / 1440 + 72px);
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

.cloud-img {
  position: relative;
  display: block;
  max-width: none;
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
