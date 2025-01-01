<script setup>
import { onMounted } from 'vue'
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";


gsap.registerPlugin(ScrollTrigger);

onMounted(() => {

  let mm = gsap.matchMedia()

  mm.add(
    {
      // set up any number of arbitrarily-named conditions. The function below will be called when ANY of them match.
      isXlAndUp: '(min-width: 1280px)',
      isLg: '(min-width: 1024px) and (max-width: 1279px)',
    },
    (context) => {
      // context.conditions has a boolean property for each condition defined above indicating if it's matched or not.
      let { isXlAndUp, isLg } = context.conditions;

      console.log("context is", isXlAndUp, "isXlAndUp is", isXlAndUp, "isLg is", isLg)

      // gsap.to(".box", {
      //   rotation: isDesktop ? 360 : 180, // spin further if desktop
      //   duration: reduceMotion ? 0 : 2, // skip to the end if prefers-reduced-motion
      // });

      if (isXlAndUp) {


        gsap.to("#baloon4", { y: -300, duration: 14, ease: 'power1.inOut' });
        gsap.to("#baloon5", { y: -300, duration: 13, ease: 'power1.inOut' });

        gsap.to("#baloon4", { y: -304, duration: 1, delay: 14, repeat: -1, yoyo: true, repeatDelay: 0.5, ease: 'slow' });
        gsap.to("#baloon5", { y: -307, duration: 1, delay: 13, repeat: -1, yoyo: true, repeatDelay: 0.7, ease: 'slow' });


        gsap.to("#baloon1", { y: -500, duration: 18, ease: 'power1.inOut' });
        gsap.to("#baloon2", { y: -500, duration: 14, ease: 'power1.inOut' });
        gsap.to("#baloon3", { y: -500, duration: 16, ease: 'power1.inOut' });

        gsap.to("#baloon4", { y: -300, duration: 14, ease: 'power1.inOut' });
        gsap.to("#baloon5", { y: -300, duration: 13, ease: 'power1.inOut' });

        gsap.to("#baloon4", { y: -304, duration: 1, delay: 14, repeat: -1, yoyo: true, repeatDelay: 0.5, ease: 'slow' });
        gsap.to("#baloon5", { y: -307, duration: 1, delay: 13, repeat: -1, yoyo: true, repeatDelay: 0.7, ease: 'slow' });
      }

      gsap.from("#baloon1", { opacity:'0%' });
      gsap.to("#baloon1", { opacity: '100%', duration: 1, delay: 0, ease: 'power1.in' });
      gsap.from("#baloon2", { opacity:'0%' });
      gsap.to("#baloon2", { opacity: '100%', duration: 1, delay: 0, ease: 'power1.in' });
      gsap.from("#baloon3", { opacity:'0%' });
      gsap.to("#baloon3", { opacity: '100%', duration: 1, delay: 0, ease: 'power1.in' });
      gsap.from("#baloon4", { opacity:'0%' });
      gsap.to("#baloon4", { opacity: '100%', duration: 1, delay: 0, ease: 'power1.in' });
      gsap.from("#baloon5", { opacity:'0%' });
      gsap.to("#baloon5", { opacity: '100%', duration: 1, delay: 0, ease: 'power1.in' });


      gsap.to("#baloon1", { y: -500, duration: 18, ease: 'power1.inOut' });
      gsap.to("#baloon2", { y: -500, duration: 14, ease: 'power1.inOut' });
      gsap.to("#baloon3", { y: -500, duration: 16, ease: 'power1.inOut' });


      gsap.from("#baloon6", { opacity: '0%' });
      gsap.from("#cloud4", { opacity:'0%' });
      gsap.to("#baloon6", { opacity: '100%', duration: 1, delay: isXlAndUp ? 9.8 : 0, ease: 'power1.in' });
      gsap.to("#baloon6", { y: -3, duration: 1, delay: isXlAndUp ? 9.5 : 0, repeat: -1, yoyo: true, repeatDelay: 0.5, ease: 'slow' });
      gsap.to("#cloud4", { opacity: '100%', duration: 1, delay: isXlAndUp ? 9.5 : 0, ease: 'power1.in' });
      
      gsap.from("#baloon7", { opacity: '0%' });
      gsap.from("#cloud5", { opacity:'0%' });
      gsap.to("#baloon7", { opacity: '100%', duration: 1, delay: isXlAndUp ? 11 : 0, ease: 'power1.in' });
      gsap.to("#baloon7", { y: -3, duration: 1, delay: isXlAndUp ? 10.7 : 0, repeat: -1, yoyo: true, repeatDelay: 0.5, ease: 'slow' });
      gsap.to("#cloud5", { opacity: '100%', duration: 1, delay: isXlAndUp ? 10.7 : 0, ease: 'power1.in' });

      gsap.to("#logo-baloon", { y: -2, duration: 1.7, delay: 0, repeat: -1, yoyo: true, repeatDelay: 0.3, ease: 'slow' });

      return () => {
        // optionally return a cleanup function that will be called when none of the conditions match anymore (after having matched)
        // it'll automatically call context.revert() - do NOT do that here . Only put custom cleanup code here.
      };
    }
  );

});

  // gsap.to("#baloon1", { y: -504, duration: 1, delay: 9, repeat: -1, yoyo: true, repeatDelay: 0.5, ease: 'slow' });
  // gsap.to("#baloon2", { y: -507, duration: 1, delay: 13, repeat: -1, yoyo: true, repeatDelay: 0.7, ease: 'slow' });
  // gsap.to("#baloon3", { y: -505, duration: 1, delay: 13, repeat: -1, yoyo: true, repeatDelay: 1.1, ease: 'slow' });

</script>

<template>
  <div class="animation-wrapper"> 
    <img id="baloon1" class="absolute hidden xl:block right-[75px] top-[250px] z-[5]" src="../assets/baloon1.svg">
    <img id="baloon2" class="absolute hidden min-[1100px]:block right-[-60px] xl:right-[-20px] top-[300px] z-[5]" src="../assets/baloon2.svg">
    <img id="baloon3" class="absolute hidden xl:block right-[200px] top-[280px] z-[5]" src="../assets/baloon3.svg">

    <img id="baloon4" class="absolute hidden xl:block right-[135px] top-[450px] z-[5] w-[70px]" src="../assets/baloon2.svg">
    <img id="baloon5" class="absolute hidden xl:block right-[20px] top-[500px] z-[5]" src="../assets/baloon3.svg">

    <img id="cloud1" class="absolute hidden xl:block right-[155px] top-[100px] z-[2]" src="../assets/cloud1.svg">
    <img id="cloud2" class="absolute hidden xl:block right-[75px] top-[20px] z-[1]" src="../assets/cloud2.svg">
    <img id="cloud3" class="absolute hidden xl:block right-[-20px] top-[100px] z-[3]" src="../assets/cloud3.svg">
    
    <img id="baloon6" class="absolute hidden lg:block right-[-50px] min-[1100px]:right-[30px]   xl:right-[240px] top-[225px] xl:top-[325px] z-[5]" src="../assets/baloon4.svg">
    <img id="cloud4" class="absolute hidden lg:block right-[-90px] min-[1100px]:right-[-10px] xl:right-[200px] top-[300px] xl:top-[400px] z-[3]" src="../assets/cloud4.svg">

    <img id="baloon7" class="absolute hidden lg:block right-[0] top-[500px] xl:right-[15px]  xl:top-[455px] z-[5]" src="../assets/baloon5.svg">
    <img id="cloud5" class="absolute hidden lg:block right-[-55px] top-[450px] xl:right-[10px]  xl:top-[500px] z-[3]" src="../assets/cloud5.svg">
  </div>
</template>