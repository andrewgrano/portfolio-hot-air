<script setup>
import logos from './components/logos.vue'
import badge from './components/badge.vue'
import timelineItem from './components/timelineItem.vue'
import pageFooter from './components/pageFooter.vue'
import bentoPortfolio from './components/BentoPortfolio.vue'

import { ref, onMounted } from 'vue'
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);

defineProps({
  name: String,
  description: String,
  imgSrc: String,
})

const timelineItems = ref([
{
    years: '2025',
    title: 'UI/UX Developer',
    company: 'Pantheon Data',
    description: 'Sole designer/developer creating the front-end of AI software for the United States Navy as an official government contractor with a security clearance. Used Typescript, React, Tanstack Table, Vite, Figma.'
  },
{
    years: '2021 - 2025',
    title: 'Front End Developer',
    company: 'ycode',
    description: 'Developed a no-code website builder platform, which enabled users to create advanced websites with an intuitive UI instead of coding. Implemented no-code animations using GSAP, created slider and lightbox components for users to customize, and created figma-like design options using Tailwind CSS.'
  },
  {
    years: '2020 - 2021',
    title: 'E-commerce Developer',
    company: 'Netalico (Agency)',
    description: 'Built and maintained e-commerce Shopify sites for high-profile clients. Developed custom sites independently. Also worked on existing sites to enhance conversions, SEO, load times, and accessibility.',
  },
  {
    years: '2019 - 2020',
    title: 'Front End Developer & UX Designer',
    company: 'WeaveUp',
    description: 'Developed and designed software for uploading, customizing, and purchasing textile designs. The company successfully exited.',
  },
  {
    years: '2018 - 2019',
    title: 'Mentor & Teacher',
    company: 'Cal State Northridge',
    description: 'Mentored & led a team of students in an Agile Scrum environment developing Vue.js applications for the campus. Created a custom style guide and component library for these projects. Also taught front-end development bootcamps and classes.',
  },
  {
    years: '2014 - 2017',
    title: 'Front End Developer',
    company: 'Fluent (Agency)',
    description: 'Built custom responsive e-commerce websites, landing pages, and web apps. Worked with a small team to successfully launch many high-converting websites.',
  },
  {
    years: '2012 - 2013',
    title: 'Theme Developer & Designer',
    company: 'DecoNetwork',
    description: 'Designed and developed custom e-commerce websites/themes for the DecoNetwork platform. Managed many projects independently and worked directly with clients.',
  },
  {
    years: '2012',
    title: 'Web Design Intern',
    company: 'Tough Guppy Productions',
    description: 'Built and maintained marketing websites for clients, primarily using WordPress. As an intern, learned about web design and development, agency work, and client relations.'
  },
  {
    years: '2008 - 2012',
    title: 'Student',
    company: 'Cal State Northridge',
    description: 'Studied Multimedia; web design, graphic design, programming, animation, and video editing.',
  },
])

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {

  gsap.fromTo(
    "#frame",
    { marginBottom: "-100vh" }, // Starting state
    {
      marginBottom: "0vh", // Ending state
      duration: 1,
      scrollTrigger: {
        trigger: "#frame",
        start: "center top",
        toggleActions: "play none none none", // Play the animation once on scroll
        scrub: true, // Sync animation with scroll progress
      },
    }
  );

  // Coordinated footer animation
  gsap.fromTo(
    "footer",
    { marginBottom: "0vh" }, // Starting state
    {
      marginBottom: "30vh", // Ending state - footer moves up
      duration: 1,
      scrollTrigger: {
        trigger: "#frame",
        start: "center top",
        toggleActions: "play none none none", // Play the animation once on scroll
        scrub: true, // Sync animation with scroll progress
      },
    }
  );

  // Animate hand-drawn highlights
  const highlights = document.querySelectorAll('.hand-drawn-highlight');
  
  // Set initial state
  gsap.set(highlights, {
    '--highlight-width': '0%'
  });
  
  // Animate the highlights
  gsap.to(highlights, {
    '--highlight-width': '100%',
    duration: 0.8,
    ease: "power2.out",
    stagger: 0.3, // 0.3 second delay between each highlight
    delay: 0.5 // Start 0.5 seconds after page load
  });

});

</script>

<template>
   <div id="frame" class="bg-[#ECECEC] rounded-3xl max-w-[1340px] mx-auto pt-[35px] pb-[50px] sm:pb-[125px] relative">
      <div class="md:px-[40px] lg:px-[75px]"> <!--  container -->
        <section class="relative">
          <div class="flex flex-col xl:flex-row mb-[15px]">
            <div class="md:mr-[25px] lg:mr-[90px]">
              <h1 class="font-['Permanent_Marker'] leading-[0.8] sm:leading-none text-[55px] sm:text-[65px] md:text-[70px] lg:text-[77px]  mb-4">
                <div>
                  <span class="text-[65px] sm:text-[75px] md:text-[80px] lg:text-[88px]">A</span>ndrew <br class="block sm:hidden"> 
                  <span class="text-[65px] sm:text-[75px] md:text-[80px] lg:text-[88px]">G</span>rano
                </div>
                <svg class="hidden sm:block w-[490px] md:w-[525px] lg:w-[568px]" width="568" height="19" viewBox="0 0 568 19" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M4 10.5456C45.8383 10.5456 130.538 7.33102 174.3 4.87138C203.831 3.2116 232.82 4.01902 377.647 6.47867C427.801 7.33046 456.867 13.7602 508.714 14.6125C520.233 13.8089 525.055 12.2016 531.557 11.3736C538.059 10.5456 546.096 10.5456 564.117 5.67502" stroke="#F5C15A" stroke-width="7" stroke-linecap="round"/>
                </svg>

                <svg class="block sm:hidden" width="200" height="19" viewBox="0 0 200 19" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M4 10.5456C45.8383 10.5456 130.538 7.33102 174.3 4.87138C203.831 3.2116 232.82 4.01902 377.647 6.47867C427.801 7.33046 456.867 13.7602 508.714 14.6125C520.233 13.8089 525.055 12.2016 531.557 11.3736C538.059 10.5456 546.096 10.5456 564.117 5.67502" stroke="#F5C15A" stroke-width="7" stroke-linecap="round"/>
                </svg>


              </h1>
              <h2 class="leading-none text-[30px] md:text-[34px] lg:text-[41px]">UI/UX Developer<br class="block sm:hidden"> & Designer.</h2>
              <!-- <hr class="bg-[#F5C15A] w-full h-[7px] border-none rounded-[20px] mt-[20px] mb-[35px]"> -->
            </div>
            <div class="flex flex-col sm:flex-row items-center gap-2 xl:mt-[-25px] xl:ml-[-35px] 2xl:ml-0 mb-[65px] xl:mb-0 mt-[25px] xl:mt-0">
              <div class="xl:mt-[-15px] mb-[25px] mb-[-30px]">
                <img class="max-w-[250px]" src="./assets/andrew-portrait.png" alt="Andrew Grano smiling">
              </div>
              <div class="relative block rotate-[-90deg]  xl:rotate-[0] w-[250px] h-[250px] top-[50px] xl:top-[100px] right-[30px] sm:right-[-25px] xl:right-[40px]">
                
                <!-- Front-End Development -->
                <div class="absolute top-[-25px] right-[-30px] 2xl:top-[-30px] 2xl:right-[-50px] w-[225px] h-[225px] rounded-full flex items-center justify-center z-10">
                  <p class="rotate-[65deg] xl:rotate-0 font-['Permanent_Marker'] text-[25px] text-center leading-tight ml-[30px] mt-[-25px] xl:mt-[-35px] xl:ml-[5px]">Front-End<br/>Development</p>
                </div>
                <!-- UI/UX Design -->
                <div class="absolute top-[105px] right-[40px] 2xl:top-[110px] 2xl:right-[25px] w-[225px] h-[225px] rounded-full flex items-center justify-center z-20">
                  <p class="rotate-[65deg] xl:rotate-0  font-['Permanent_Marker'] text-[25px] text-center leading-tight mt-[10px] ml-[-5px] xl:ml-0">UI/UX<br/>Design</p>
                </div>

                <!-- Arrow pointing to overlap -->
                <div class="absolute right-[30px] top-[165px] 2xl:top-[170px] 2xl:right-[5px] z-[100]">
                  <svg width="58" height="33" viewBox="0 0 58 33" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M3.972 16.6106C4.10383 15.7533 4.08384 13.9908 3.77407 12.177C3.46429 10.3633 3.15568 8.55638 2.77483 6.73171C2.67486 6.25279 2.40728 5.79545 2.5297 5.44386C3.10751 3.7844 5.86204 4.26299 7.67577 3.95322C9.48951 3.64344 11.2964 3.33483 13.1102 3.02506C13.5653 2.94732 14.0136 2.87075 14.4756 2.79186" stroke="black" stroke-width="5" stroke-linecap="round"/>
                    <path d="M4 6.37695C6.34472 7.3461 12.1477 12.4855 17.615 16.0431C22.9944 19.5433 28.149 21.4964 32.939 24.0775C37.5903 25.4283 42.2007 26.5656 47.5376 27.4217C49.4081 27.4226 51.9705 27.1338 54.6105 26.8362" stroke="black" stroke-width="5" stroke-linecap="round"/>
                  </svg>
                </div>

                <span class="rotate-90 xl:rotate-0  font-['Permanent_Marker'] leading-[25px] text-[#2D2D2D] text-[25px] absolute top-[212px] right-[-41px] xl:top-[180px] xl:right-[-65px] 2xl:top-[190px] 2xl:right-[-90px]">Andrew<br/>Grano</span>

                <!-- Venn Diagram Image -->
                <svg class="relative top-[-30px] w-[264px] 2xl:w-[300px]" width="300" height="365" viewBox="43 43 303 365" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <circle cx="231.409" cy="155.956" r="110" transform="rotate(-56.4072 231.409 155.956)" fill="#40D395" fill-opacity="0.3" stroke="#40D395" stroke-width="5"/>
                  <circle cx="155.956" cy="293.956" r="110" transform="rotate(-56.4072 155.956 293.956)" fill="#F5C15A" fill-opacity="0.3" stroke="#F5C15A" stroke-width="5"/>
                  <circle cx="231.409" cy="155.956" r="110" transform="rotate(-56.4072 231.409 155.956)" fill="#4FC565" fill-opacity="0.3" stroke="#4FC565" stroke-width="5"/>
                  <circle cx="155.956" cy="293.956" r="110" transform="rotate(-56.4072 155.956 293.956)" fill="#F5C15A" fill-opacity="0.3" stroke="#F5C15A" stroke-width="5"/>
                  <mask id="path-5-inside-1_165_230" fill="white">
                  <path d="M123 185.915C154.058 176.449 188.949 180.434 218.106 199.801C241.471 215.32 257.157 238.064 264.175 263.108C233.117 272.573 198.226 268.59 169.069 249.224C145.704 233.704 130.018 210.96 123 185.915Z"/>
                  </mask>
                  <path d="M123 185.915C154.058 176.449 188.949 180.434 218.106 199.801C241.471 215.32 257.157 238.064 264.175 263.108C233.117 272.573 198.226 268.59 169.069 249.224C145.704 233.704 130.018 210.96 123 185.915Z" fill="#BDD2E0"/>
                  <path d="M123 185.915L122.125 183.045L119.32 183.901L120.111 186.725L123 185.915ZM218.106 199.801L219.766 197.302L219.766 197.302L218.106 199.801ZM264.175 263.108L265.049 265.977L267.855 265.122L267.064 262.298L264.175 263.108ZM169.069 249.224L167.409 251.723L167.409 251.723L169.069 249.224ZM123 185.915L123.875 188.785C154.111 179.569 188.068 183.45 216.447 202.3L218.106 199.801L219.766 197.302C189.831 177.418 154.004 173.329 122.125 183.045L123 185.915ZM218.106 199.801L216.447 202.3C239.19 217.406 254.455 239.539 261.286 263.917L264.175 263.108L267.064 262.298C259.859 236.589 243.752 213.234 219.766 197.302L218.106 199.801ZM264.175 263.108L263.3 260.238C233.064 269.453 199.107 265.574 170.729 246.725L169.069 249.224L167.409 251.723C197.345 271.606 233.171 275.693 265.049 265.977L264.175 263.108ZM169.069 249.224L170.729 246.725C147.985 231.618 132.72 209.484 125.889 185.106L123 185.915L120.111 186.725C127.316 212.435 143.423 235.791 167.409 251.723L169.069 249.224Z" fill="#4F94C5" mask="url(#path-5-inside-1_165_230)"/>
                </svg>

              </div>
            </div>
          </div>

          <div class="relative hidden lg:block">
           
            
          </div>

          <div class="flex flex-col gap-[20px] mb-[50px] tracking-[-0.03rem] leading-tight">
            <p>Specialized in working at the intersection of <strong class="hand-drawn-highlight">design & development</strong>.</p>
            <p>Creates web sites & web apps that are <strong class="hand-drawn-highlight">accessible, functional & beautiful</strong>.</p>
            <p>A strong <strong class="hand-drawn-highlight">communicator and problem solver</strong> with <strong class="hand-drawn-highlight">12+ years</strong> of experience.</p>
            <!-- <p>A <strong>problem solver</strong> with an eclectic <strong>12 year</strong> professional history, and a lifetime passion.</p> -->
            <!-- <p>A <strong>problem solver</strong> who enjoys <strong>crafting design systems</strong> and building <strong>responsive layouts</strong>.</p> -->
          </div>

          <div class="flex flex-col block lg:hidden">
            <h3 class="sectionHeading ">Projects</h3>
            <svg width="125" height="10" viewBox="0 0 125 10" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M3 5.10549C7.26041 5.10549 16.7287 4.68869 21.0245 3.94983C26.0631 3.08323 30.0642 3.63408 35.285 3.31833C48.3512 2.52808 57.7794 3.41937 60.0224 3.73512C67.379 4.77072 74.6986 4.47398 81.824 4.99813C89.9898 5.59881 93.8543 5.73699 97.0931 6.36534C98.4227 6.62329 106.055 7 118.817 7C133.837 7 137.258 6.36849 140.915 5.84435C146.674 5.01921 152.701 5.10549 165.543 4.58134C174.692 4.20796 192.353 4.47398 201.766 4.36978C211.822 4.25847 219.282 3.84248 229.913 3.94667C240.365 4.04911 252.424 4.89077 255.753 5.62963C257.739 6.07045 259.52 5.94539 266.443 6.26114C272.721 6.54752 284.638 6.36849 291.093 6.2643C298.186 5.9517 299.482 5.52859 300.874 5.10864C301.628 4.89709 302.479 4.68869 304 3.84248" stroke="#F5C15A" stroke-width="5" stroke-linecap="round"/>
            </svg>
          </div>

          <bentoPortfolio />


          <div class="flex flex-col mb-[50px]">
            <h3 class="sectionHeading ">Skills & Qualifications</h3>
            <svg width="307" height="10" viewBox="0 0 307 10" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M3 5.10549C7.26041 5.10549 16.7287 4.68869 21.0245 3.94983C26.0631 3.08323 30.0642 3.63408 35.285 3.31833C48.3512 2.52808 57.7794 3.41937 60.0224 3.73512C67.379 4.77072 74.6986 4.47398 81.824 4.99813C89.9898 5.59881 93.8543 5.73699 97.0931 6.36534C98.4227 6.62329 106.055 7 118.817 7C133.837 7 137.258 6.36849 140.915 5.84435C146.674 5.01921 152.701 5.10549 165.543 4.58134C174.692 4.20796 192.353 4.47398 201.766 4.36978C211.822 4.25847 219.282 3.84248 229.913 3.94667C240.365 4.04911 252.424 4.89077 255.753 5.62963C257.739 6.07045 259.52 5.94539 266.443 6.26114C272.721 6.54752 284.638 6.36849 291.093 6.2643C298.186 5.9517 299.482 5.52859 300.874 5.10864C301.628 4.89709 302.479 4.68869 304 3.84248" stroke="#F5C15A" stroke-width="5" stroke-linecap="round"/>
            </svg>

          </div>

          <div class="flex flex-col gap-[20px] mb-[50px]">
            <div class="flex gap-[10px] flex-wrap">
              <!-- <badge text="12+ years experience" color="blue" first="true"/> -->
              <badge text="B.A. Degree, Multimedia" color="blue"/>
              <badge text="LearnUI.Design Cert." color="blue"/>
              <badge text="Govt. Security Clearance" color="blue" />
              <!-- <badge text="Teaching / Mentoring" color="blue"/> -->
            </div>
            <div class="flex gap-[10px] flex-wrap">
              <badge text="Javascript / Typescript" color="green" first="true"/>
              <!-- <badge text="Typescript" color="green" first="true"/> -->
              <badge text="React" color="green" first="true"/>
              <badge text="Vue.js" color="green" first="true"/>
              <badge text="Tailwind CSS" color="green"/>
              <!-- <badge text="GSAP Animations" color="green"/> -->
              <!-- <badge text="AI Tools" color="green"/> -->
              <!-- <badge text="Vite" color="green"/> -->
              <badge text="Git & Github" color="green"/> 
            </div>
            <div class="flex gap-[10px] flex-wrap">
              <!-- <badge text="Front End Development" color="yellow"/> -->
              
              <badge text="Figma" color="yellow" first="true"/>
              <badge text="Responsive Design" color="yellow"/>
              <badge text="Wireframing" color="yellow"/>
              <badge text="Styleguides" color="yellow"/>
              <badge text="Animations" color="yellow"/>
             
            </div>
            <div class="flex gap-[10px] flex-wrap">
              <!-- <badge text="12+ years experience" color="blue"/> -->
              <badge text="AI & No-Code Tools" color="blue"/>
              <badge text="Shopify & E-commerce" color="blue"/>
              <badge text="Teaching / Mentoring" color="blue"/>
              <!-- <badge text="Agile Scrum" color="blue"/> -->

            </div>
            
          </div>
        </section>


        <logos />

        
        <section>
          <div class="mb-[50px]">
            <h3 class="sectionHeading">Professional History</h3>
            <svg width="266" height="10" viewBox="0 0 266 10" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M2.9668 5.27994C6.64181 5.27994 14.8091 4.91299 18.5147 4.2625C22.8609 3.49955 26.3123 3.98451 30.8157 3.70652C42.0865 3.01079 50.2193 3.79548 52.1541 4.07347C58.4998 4.98521 64.8137 4.72396 70.96 5.18542C78.0038 5.71426 81.3373 5.83592 84.1311 6.38911C85.278 6.61621 91.862 6.94787 102.87 6.94787C115.826 6.94787 118.777 6.39189 121.932 5.93043C126.899 5.20398 132.098 5.27994 143.176 4.81848C151.067 4.48975 166.302 4.72396 174.422 4.63223C183.096 4.53423 189.53 4.16799 198.701 4.25972C207.717 4.3499 218.119 5.09091 220.99 5.7414C222.704 6.12949 224.24 6.01939 230.211 6.29738C235.627 6.54951 245.907 6.39189 251.475 6.30016C257.593 6.02495 258.711 5.65244 259.912 5.28272C260.562 5.09647 261.296 4.91299 262.608 4.16799" stroke="#F5C15A" stroke-width="5" stroke-linecap="round"/>
            </svg>
          </div>


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
.hand-drawn-highlight {
  position: relative;
  display: inline;
}

.hand-drawn-highlight::after {
  content: '';
  position: absolute;
  left: -2px;
  right: -2px;
  top: 0;
  bottom: 0;
  background-color: #F5C15A;
  z-index: -1;
  border-radius: 3px 8px 8px 3px;
  transform: rotate(-0.5deg);
  opacity: 0.8;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  z-index: 1;
  mix-blend-mode: darken;
  width: var(--highlight-width, 0%); /* Use CSS custom property */
  overflow: hidden; /* Hide overflow during animation */
}

.hand-drawn-highlight:nth-child(2n)::after {
  transform: rotate(2deg);
}

</style>
