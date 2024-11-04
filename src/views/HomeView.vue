<template>
  <div class="home-view" :class="{ 'fade-in': isVisible }">
    <header class="header">
      <h1>Bienvenue dans le Mémorial</h1>
      <RadialMenuComp /> <!-- Menu radial en haut à droite -->
    </header>
    <main class="main-content">
      <!-- Section À Propos -->
      <section class="about-section">
        <h2>À Propos</h2>
        <p>Ce site est dédié pour honorer et préserver la mémoire...</p>
      </section>

      <!-- Section Galerie -->
      <section class="gallery-section">
        <h2>Galerie de Souvenirs</h2>
        <!-- Placeholder pour les images ou souvenirs -->
        <div class="gallery">
          <!-- Ajoutez ici des images pour la galerie -->
        </div>
      </section>
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import RadialMenuComp from '@/components/RadialMenuComp.vue';

const isVisible = ref(false);

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true; // Déclenche le fade-in après le montage
  }, 100); // Délai court pour initier la transition
});
</script>

<style scoped>
.home-view {
  opacity: 0; /* Initialement invisible pour le fade-in */
  background-image: url('/img/img4.webp'); /* Image de fond */
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  min-height: 100vh;
  padding: 20px;
  color: #ffffff;
  transition: opacity 1.5s ease-in-out; /* Durée du fade-in */
}

.fade-in {
  opacity: 1; /* Visible une fois le fade-in terminé */
}

.header {
  position: relative;
  text-align: center;
  margin-top: 20px;
}

/* Positionne le menu radial en haut à droite */
.header > :first-child {
  position: absolute;
  top: 0;
  right: 0;
  margin: 20px;
}

.header > :last-child{
  margin-top: 80px;
}



.main-content {
  padding: 20px;
  background-color: rgba(0, 0, 0, 0.5); /* Fond semi-transparent pour le texte */
  border-radius: 10px;
}

.about-section, .gallery-section {
  margin-bottom: 40px;
}

.gallery {
  display: grid;
  gap: 15px;
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  margin-top: 20px;
}
</style>
