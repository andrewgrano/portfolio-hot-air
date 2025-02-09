<script setup>
import logos from './components/logos.vue'
import badge from './components/badge.vue'
import portfolioItem from './components/portfolioItem.vue'
import timelineItem from './components/timelineItem.vue'
import baloonAnimations from './components/baloonAnimations.vue'
import pageFooter from './components/pageFooter.vue'

import { ref, onMounted } from 'vue'
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);

defineProps({
  name: String,
  description: String,
  imgSrc: String,
})

const porfolioItems = ref([
  {
    name: 'Roaming Love',
    description: 'Editorial / Travel Blog',
    imgSrc: '/screenshot-romainglove.jpg',
    url: 'https://www.roaminglove.com/',
  },
  {
    name: 'InfoPacked',
    description: 'Template / Landing Page',
    imgSrc: '/screenshot-infopacked.jpg',
    url: 'https://infopacked.ycode.site/',
  },
  {
    name: 'CSUN Styleguide',
    description: 'Style Guide',
    imgSrc: '/screenshot-metaphor.jpg',
    url: 'https://metaphor-v2.netlify.app/documentation/',
  },
  {
    name: 'Picture Day Company',
    description: 'Landing Page',
    imgSrc: '/screenshot-pdc.jpg',
    url: 'https://thepicturedaycompany.com/',
  },
  {
    name: 'PB Cottages',
    description: 'Landing Page',
    imgSrc: '/screenshot-pbcottages.jpg',
    url: 'https://pacificbeachcottages.com/',
  },
  {
    name: 'Media Kit for Roaming Love',
    description: 'Landing Page',
    imgSrc: '/screenshot-mediakit.jpg',
    url: 'http://mediakit.roaminglove.com/',
  },
])


const timelineItems = ref([
{
    years: '2021 - Current',
    title: 'Front End Developer',
    company: 'ycode',
    description: 'Developed a no-code website builder platform, which enabled users to create advanced websites with an intuitive UI instead of coding. Implemented no-code animations using GSAP, created slider and lightbox components for users to customize, and created figma-like design options using Tailwind CSS.'
  },
  {
    years: '2020 - 2021',
    title: 'E-commerce Developer',
    company: 'Netalico (Agency)',
    description: 'Built and maintained e-commerce Shopify sites for high profile clients. Developed custom sites independently. Also worked on existing sites to enhance conversions, SEO, load times, and accessibility.',
  },
  {
    years: '2019 - 2020',
    title: 'Front End Developer & UX Designer',
    company: 'WeaveUp',
    description: 'Developed and designed software for uploading, customizing and purchasing textile designs. The company successfully exited.',
  },
  {
    years: '2018 - 2019',
    title: 'Mentor & Teacher',
    company: 'Cal State Northridge',
    description: 'Mentored & led a team of students in an agile SCRUM environment developing Vue.JS applications for the campus. Created a custom style guide / component library for these projects. Also taught front-end development bootcamps and classes.',
  },
  {
    years: '2014 - 2017',
    title: 'Front End Developer',
    company: 'Fluent (Agency)',
    description: 'Built custom responsive e-commerce websites, landing pages, and web apps. Worked with a small team to successfully launch many high converting websites.',
  },
  {
    years: '2012 - 2013',
    title: 'Theme Developer & Designer',
    company: 'DecoNetwork',
    description: 'Designed and developed custom e-commerce websites/themes for the DecoNetwork platform. Self-managed many projects and worked directly with clients.',
  },
  {
    years: '2012',
    title: 'Web Design Intern',
    company: 'Tough Guppy Productions',
    description: 'Built and maintained marketing websites for clients, primarily using WordPress. As an intern, learned about web design and development, agency work, and client relations.'
  },
  {
    years: '2008 - 2012',
    title: 'Student - Multimedia',
    company: 'Cal State Northridge',
    description: 'Studied web design, graphic design, programming, animation and video editing.',
  },
])

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {

  gsap.fromTo(
    "#frame",
    { marginBottom: "-25vh" }, // Starting state
    {
      marginBottom: "0px", // Ending state
      duration: 1,
      scrollTrigger: {
        trigger: "#frame",
        start: "center top", // When the bottom of #frame hits the bottom of the viewport
        toggleActions: "play none none none", // Play the animation once on scroll
        scrub: true, // Sync animation with scroll progress
      },
    }
  );

});

</script>

<template>
   <div id="frame" class="bg-white rounded-3xl max-w-[1340px] mx-auto pt-[35px] pb-[50px] sm:pb-[125px] relative">
      <div class="md:px-[40px] lg:px-[75px]"> <!--  container -->
        <section class="relative">
          <baloonAnimations />

          <div class="flex flex-col sm:flex-row">
            <div class="md:mr-[25px] lg:mr-[70px]">
              <h1 class="font-bold leading-none text-[55px] sm:text-[65px] md:text-[70px] lg:text-[78px]">Andrew Grano</h1>
              <h2 class="text-[39px] leading-none text-[34px]  md:text-[43px] lg:text-[52px] lg:text-[#686868]">UI Developer & Designer</h2>
              <hr class="bg-[#F5C15A] w-full h-[7px] border-none rounded-[20px] mt-[20px] mb-[35px]">
            </div>
            <div class="mt-[-15px] mb-[25px] lg:mb-[-30px] mr-auto sm:mr-none sm:ml-auto lg:ml-0">
              <img class="max-w-[200px] lg:max-w-[250px]" src="./assets/andrew-portrait.png" alt="Andrew Grano smiling">
            </div>
          </div>

          <div class="flex flex-col gap-[25px] mb-[40px]">
            <p>Specialized in working at the <strong>intersection</strong> of <strong>design & development</strong>.</p>
            <p>Experienced in creating <strong>web sites & web apps</strong> that are <strong>accessible, functional & beautiful</strong>.</p>
            <p>A <strong>problem solver</strong> who enjoys <strong>crafting design systems</strong> and building <strong>responsive layouts</strong>.</p>
            <p>With skills and qualifications that include...</p>
          </div>

          <div class="flex flex-col gap-[20px]">
            <div class="flex gap-[10px] flex-wrap sm:flex-nowrap">
              <badge text="Javascript" color="green" first="true"/>
              <badge text="React" color="green" first="true"/>
              <badge text="Vue.js" color="green" first="true"/>
              <badge text="Tailwind CSS" color="green"/>
              <badge text="SCSS" color="green"/>
              <badge text="GSAP Animations" color="green"/>
            </div>
            <div class="flex gap-[10px] flex-wrap sm:flex-nowrap">
              <!-- <badge text="Front End Development" color="yellow"/> -->
              <badge text="Figma" color="yellow" first="true"/>
              <badge text="Shopify & E-Commerce" color="yellow" />
              <badge text="UI/UX" color="yellow"/>
              <badge text="Teaching / Mentoring" color="yellow"/>
              <badge text="No-code" color="yellow"/>
            </div>
            <div class="flex gap-[10px] flex-wrap sm:flex-nowrap">
              <badge text="12+ years experience" color="blue" first="true"/>
              <badge text="B.A. Degree in Multimedia" color="blue"/>
              <badge text="LearnUI.Design Graduate" color="blue"/>
            </div>
          </div>
        </section>

        <logos />

        <section class="mb-[125px]">
          <h3 class="sectionHeading">Portfolio</h3>
          <p class="mb-[60px]">A sampling of projects I’ve designed and developed myself.
            <!-- <br> <em class="opacity-50">(I also have experience working with teams on larger projects; see farther below)</em> -->
          </p>

          <ul role="list" class="grid grid-cols-1 sm:grid-cols-2 gap-x-4 gap-y-12 lg:grid-cols-3 sm:gap-x-6 xl:gap-x-8">
            <portfolioItem
              v-for="(item, index) in porfolioItems"
              :key="index"
              :name="item.name"
              :description="item.description"
              :img-src="item.imgSrc"
              :url="item.url"
            />
          </ul>
        </section>
        <section>
          <h3 class="sectionHeading">Professional History</h3>
          <p class="mb-[60px]">Details about my 12+ years of experience.</p>

          <ul class="flex flex-col items-center">
            <timelineItem
              v-for="(item, index) in timelineItems"
              :key="index"
              :index="index"
              :is-last="index === timelineItems?.length - 1"
              :years="item.years"
              :title="item.title"
              :company="item.company"
              :description="item.description"
            />
          </ul>
        </section>
      </div>
  </div>
  <pageFooter />
</template>

<style scoped>

</style>
