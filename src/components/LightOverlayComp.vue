<!-- src/components/LightOverlayComp.vue -->
<template>
  <div class="light-overlay"></div>
</template>

<script setup>
</script>

<style scoped>
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
