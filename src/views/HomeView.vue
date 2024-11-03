<template>
  <div class="wrapper">
    <div class="content">
      <HeroSectionComp />
      <GradientSectionsComp />
    </div>
    <ImageContainerComp />
    <AudioPlayerComp src="/musiques/Sarah_McLachlan-In_the_arms_of_an_angel.mp3" ref="audioPlayer" /> <!-- Utilisation du composant AudioPlayerComp -->
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import HeroSectionComp from '@/components/HeroSectionComp.vue';
import GradientSectionsComp from '@/components/GradientSectionsComp.vue';
import ImageContainerComp from '@/components/ImageContainerComp.vue';
import AudioPlayerComp from '@/components/AudioPlayerComp.vue'; // Import du composant
import { gsap } from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const audioPlayer = ref(null); // Référence pour le composant AudioPlayerComp
const audioHasPlayed = ref(false); // État pour vérifier si l'audio a déjà été joué

onMounted(() => {
  // Écouteur d'événements pour le défilement
  const handleScroll = () => {
    if (!audioHasPlayed.value) { // Vérifie si l'audio n'a pas déjà été joué
      const audio = audioPlayer.value.$refs.audio; // Accède à l'élément audio dans le composant
      if (audio) {
        audio.play().then(() => {
          audioHasPlayed.value = true; // Indique que l'audio a été joué
        }).catch((error) => {
          console.error("Error playing audio:", error); // Log de l'erreur s'il y a un problème
        });
      }
    }
    window.removeEventListener('scroll', handleScroll); // Supprime l'écouteur après le premier scroll
  };

  window.addEventListener('scroll', handleScroll); // Ajoute l'écouteur d'événements pour le scroll

  gsap
    .timeline({
      scrollTrigger: {
        trigger: ".image-container",
        start: "top top",
        end: "+=150%",
        pin: true,
        scrub: true,
        markers: false // Désactive les marqueurs
      }
    })
    .to(".light-overlay", {
      opacity: 0, // Dissipe la couche de lumière
      duration: 0.5, // Durée de l'animation
      ease: "power1.inOut"
    }, 0) // Commence à dissiper immédiatement
    .to(".fenetre", {
      scale: 20, // Zoom sur l'image de la fenêtre
      transformOrigin: "center center",
      ease: "power1.inOut"
    }, "<"); // Synchronise avec le zoom
});
</script>

<style scoped>
.wrapper {
  position: relative;
  width: 100%;
  height: 100vh;
}
.content {
  overflow-x: hidden; /* Empêche le débordement horizontal */
  overflow-y: auto; /* Permet le défilement vertical si nécessaire */
  width: 100%;
  height: 100vh; /* Remplit toute la hauteur de l'écran */
}

</style>
