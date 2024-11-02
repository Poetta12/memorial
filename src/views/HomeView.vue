<template>
  <div class="wrapper">
    <div class="content">
      <section class="section hero"></section>
      <section class="section gradient-purple"></section>
      <section class="section gradient-blue"></section>
    </div>
    <div class="image-container">
      <img src="/img/bye.webp" alt="Au revoir" class="bye" />
      <div class="light-overlay"></div> <!-- Couche de lumière -->
      <img src="/img/fenetre.png" alt="fenetre" class="fenetre" />
    </div>
    <AudioPlayerComp src="/musiques/Sarah_McLachlan-In_the_arms_of_an_angel.mp3" ref="audioPlayer" /> <!-- Utilisation du composant AudioPlayerComp -->
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
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
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  overflow: hidden; /* Désactive le défilement de la page */
}

.wrapper,
.content {
  position: relative;
  width: 100%;
  height: 100vh; /* S'assure que le wrapper remplit toute la hauteur de l'écran */
  z-index: 1;
}

.content {
  overflow-x: hidden;
}

.content .section {
  width: 100%;
  height: 100vh;
}

.content .section.hero {
  background-image: url("/img/bye.webp");
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
}

.image-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  z-index: 2;
}

.image-container img {
  position: absolute; /* Positionne les images les unes sur les autres */
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover; /* Couvre le conteneur sans déformation */
}

.bye {
  z-index: 1; /* Image de l'image en dessous */
}

.fenetre {
  z-index: 2; /* Image de la fenêtre au-dessus */
}

.light-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.8); /* Couleur de lumière pleine */
  z-index: 1; /* Entre l'image de la fenêtre et le paysage */
  transition: opacity 0.1s ease; /* Transition pour l'effet de dissipation */
}
</style>
