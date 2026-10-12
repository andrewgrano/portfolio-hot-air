<template>
  <footer class="pt-[100px] pb-[0px] text-[#2d2d2d] md:text-[#ECECEC]">
    
    <h3 class="font-['Permanent_Marker'] text-[54px] sm:text-[78px] leading-tight text-center mb-[70px] lg:mb-[100px]">
      Andrew Grano
    </h3>
    <ul class="footer-list flex flex-col md:flex-row text-center justify-center gap-[15px] md:gap-[30px] mb-[100px]">
      <li><a class="underline sm:text-[20px] md:text-[22px] footer-highlight" href="mailto:andrewgrano@gmail.com">Email</a></li>
      <li><a class="underline sm:text-[20px] md:text-[22px] footer-highlight" href="https://www.linkedin.com/in/andrewgrano/" target="linkedin">LinkedIn</a></li>
      <li><a class="underline sm:text-[20px] md:text-[22px] footer-highlight" href="/andrew-grano-resume.pdf" target="resume">Resume</a></li>
    </ul>
  </footer>
  <p class="text-[13px] opacity-[80%] text-cente text-[#2d2d2d] md:text-[#ECECEC] text-center mb-[50px]">Copyright 2026</p>

</template>

<style scoped>
.footer-highlight {
  position: relative;
  display: inline;
  transition: all 0.2s ease;
}

.footer-highlight::after {
  content: '';
  position: absolute;
  left: -2px;
  right: -2px;
  top: 0;
  bottom: 0;
  background-color: #F5C15A;
  z-index: -1;
  border-radius: 1px 1px 1px 1px;
  transform: rotate(0.3deg);
  opacity: 0;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  transition: opacity 0.2s ease;
}

.footer-highlight:hover {
  color: black;
  text-decoration: none;
  /* color: #F5C15A; */
}

.footer-highlight:hover::after {
  opacity: 0.8;
}

</style>