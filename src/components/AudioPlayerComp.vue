<!-- src/components/AudioPlayerComp.vue -->
<template>
  <audio ref="audio" :src="src" preload="auto" />
</template>

<script setup>
import { ref, defineProps } from 'vue';

const props = defineProps({
  src: {
    type: String,
    required: true,
  }
});

const audio = ref(null); // Référence à l'élément audio
</script>

<style scoped>
/* Styles spécifiques au composant AudioPlayerComp si nécessaire */
</style>
