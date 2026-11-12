<script setup>
import portrait from '../assets/footer/andrew-portrait.png'
import balloonSmall from '../assets/footer/balloon-sunset.svg'
import flameSmall from '../assets/hero/flame-small.svg'
</script>

<template>
  <footer class="site-footer">
    <div class="footer-inner">
      <div class="rule"></div>
      <ul class="links">
        <li><a href="mailto:andrewgrano@gmail.com">Email</a></li>
        <li><a href="https://www.linkedin.com/in/andrewgrano/" target="linkedin">LinkedIn</a></li>
        <li><a href="/andrew-grano-resume.pdf" target="resume">Resume</a></li>
      </ul>
      <div class="identity">
        <img :src="portrait" width="136" height="136" alt="">
        <p class="name">Andrew Grano</p>
      </div>
      <p class="copyright">© 2026</p>
    </div>
    <div class="ground" aria-hidden="true">
      <svg class="hills" viewBox="0 0 1440 220" preserveAspectRatio="none">
        <path fill="#a9b8ab" d="M0 168C180 168 320 130 480 124C680 116 860 150 1100 146C1280 142 1380 160 1440 164V220H0Z" />
        <path fill="#233e38" d="M0 200C280 200 480 168 660 132C800 108 940 128 1120 160C1280 188 1380 200 1440 204V220H0Z" />
      </svg>
      <div class="balloon">
        <img :src="balloonSmall" width="72" height="98" alt="">
        <img class="flame" :src="flameSmall" width="72" height="98" alt="">
      </div>
    </div>
  </footer>
</template>

<style scoped>
.site-footer {
  background: #F5F2EA;
  width: calc(100% + 60px);
  margin-left: -30px;
  margin-right: -30px;
  padding-top: 72px;
}

.footer-inner {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 24px;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px 56px;
}

.rule {
  width: 100%;
  height: 1px;
  background: rgba(35, 62, 56, 0.18);
}

.links {
  display: flex;
  gap: 32px;
  margin: 0;
  padding: 0;
  list-style: none;
}

.links a {
  font-family: "Instrument Sans", sans-serif;
  font-size: 14px;
  font-weight: 400;
  line-height: 1.5;
  color: #233e38;
  text-decoration: none;
}

.identity {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.identity img {
  width: 136px;
  height: 136px;
}

.name {
  margin: 0;
  font-family: "Cormorant Garamond", Georgia, serif;
  font-weight: 400;
  font-size: clamp(48px, 11vw, 73px);
  line-height: 1;
  color: #233e38;
  text-align: center;
}

.copyright {
  margin: 0;
  font-family: "Instrument Sans", sans-serif;
  font-size: 13px;
  font-weight: 400;
  line-height: 1.5;
  color: #6d7a70;
}

.ground {
  position: relative;
  height: 210px;
  overflow: hidden;
  /* Sunset held back while we see the ground on cream.
  background: linear-gradient(
    180deg,
    rgba(247, 196, 226, 0) 0%,
    rgba(247, 196, 226, 0.5) 24%,
    rgba(255, 168, 150, 0.38) 42%,
    rgba(255, 196, 150, 0.16) 62%,
    rgba(255, 206, 156, 0) 80%
  );
  */
}

.hills {
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
  display: block;
}

.balloon {
  position: absolute;
  left: 56%;
  bottom: 90px;
  z-index: 1;
  width: 72px;
  height: 98px;
  transform: translateX(-50%);
  animation: lift 5.2s ease-in-out infinite;
}

.balloon img {
  display: block;
  width: 100%;
  height: 100%;
}

.flame {
  position: absolute;
  left: 0;
  top: 0;
  animation: flicker 5.2s ease-in-out infinite;
}

@keyframes lift {
  0%, 100% { transform: translateX(-50%) translateY(0) rotate(-0.6deg); }
  50% { transform: translateX(-50%) translateY(-8px) rotate(0.8deg); }
}

@keyframes flicker {
  0%, 100% { opacity: 0.2; }
  45% { opacity: 1; }
  70% { opacity: 0.35; }
}

@media (prefers-reduced-motion: reduce) {
  .balloon,
  .flame {
    animation: none;
  }

  .flame {
    opacity: 0.65;
  }
}

@media (min-width: 768px) {
  .footer-inner {
    padding-left: max(48px, min(120px, 8.333vw));
    padding-right: max(48px, min(120px, 8.333vw));
  }
}
</style>
