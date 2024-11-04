<template>
  <div id="app">
    <HeaderComp v-if="showHeader" /> <!-- Header conditionnel -->
    <router-view v-slot="{ Component }">
      <transition name="fade">
        <component :is="Component" />
      </transition>
    </router-view>
  </div>
</template>

<script setup>
import { computed } from 'vue';
import { useRoute } from 'vue-router';
import HeaderComp from '@/components/HeaderComp.vue'; // Import du header global

const route = useRoute();
const showHeader = computed(() => route.name !== 'landing'); // Affiche le header sauf sur LandingView
</script>

<style>
/* Transition fade-in pour l'entrée de HomeView */
.fade-enter-active, .fade-leave-active {
  transition: opacity 1.5s ease; /* Durée du fade-in et du fade-out */
}

.fade-enter, .fade-leave-to {
  opacity: 0; /* Initialisation pour le fade-in et fin pour le fade-out */
}
</style>
