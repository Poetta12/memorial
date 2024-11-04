<template>
  <div class="landing-view" :class="{ 'fade-out': transitioned }">
    <div class="wrapper">
      <div class="content">
        <HeroSectionComp />
        <GradientSectionsComp />
      </div>
      <ImageContainerComp />
      <AudioPlayerComp src="/musiques/Sarah_McLachlan-In_the_arms_of_an_angel.mp3" ref="audioPlayer" />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import HeroSectionComp from '@/components/HeroSectionComp.vue';
import GradientSectionsComp from '@/components/GradientSectionsComp.vue';
import ImageContainerComp from '@/components/ImageContainerComp.vue';
import AudioPlayerComp from '@/components/AudioPlayerComp.vue';
import { gsap } from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const audioPlayer = ref(null);
const audioHasPlayed = ref(false);
const transitioned = ref(false);
const router = useRouter();

onMounted(() => {
  const handleScroll = () => {
    if (!audioHasPlayed.value && audioPlayer.value) {
      const audio = audioPlayer.value.$refs.audio;
      if (audio) {
        audio.play().then(() => {
          audioHasPlayed.value = true;
        }).catch(console.error);
      }
    }
  };

  window.addEventListener('scroll', handleScroll);

  gsap.timeline({
    scrollTrigger: {
      trigger: ".image-container",
      start: "top top",
      end: "+=100%",
      pin: true,
      scrub: true,
      onLeave: () => {
        window.removeEventListener('scroll', handleScroll);
        transitioned.value = true; // Déclenche le fade-out
        console.log("Animation terminée, redirection vers HomeView"); // Vérification
        setTimeout(() => {
          router.push('/home'); // Redirection vers HomeView après le fade-out
        }, 1000);
      },
    }
  })
    .to(".light-overlay", {
      opacity: 0,
      duration: 1.5,
      ease: "power1.inOut"
    }, 0)
    .to(".fenetre", {
      scale: 20,
      transformOrigin: "center center",
      duration: 1.5,
      ease: "power1.inOut"
    }, "<");
});
</script>

<style scoped>
.landing-view {
  transition: opacity 1.5s ease-in-out; /* Applique le fade-out */
}

.fade-out {
  opacity: 0;
}

.wrapper {
  position: relative;
  width: 100%;
  height: 100vh;
}

.content {
  overflow-x: hidden;
  overflow-y: auto;
  width: 100%;
  height: 100vh;
}
</style>
