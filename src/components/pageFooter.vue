<script setup>
import portrait from '../assets/footer/andrew-portrait.png'
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
  </footer>
</template>

<style scoped>
.site-footer {
  background: #F5F2EA;
  width: calc(100% + 60px);
  margin-left: -30px;
  margin-right: -30px;
  padding: 72px 24px;
}

.footer-inner {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 24px;
  max-width: 1200px;
  margin: 0 auto;
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

@media (min-width: 768px) {
  .site-footer {
    padding-left: max(48px, min(120px, 8.333vw));
    padding-right: max(48px, min(120px, 8.333vw));
  }
}
</style>
