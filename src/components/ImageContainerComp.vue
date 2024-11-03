<!-- src/components/ImageContainerComp.vue -->
<template>
  <div class="image-container">
    <img src="/img/bye.webp" alt="Au revoir" class="bye" />
    <LightOverlayComp />
    <img src="/img/fenetre.png" alt="fenetre" class="fenetre" />
  </div>
</template>

<script setup>
import LightOverlayComp from './LightOverlayComp.vue'; // Importer le composant LightOverlay
</script>

<style scoped>
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
</style>
