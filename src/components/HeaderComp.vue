<template>
  <header class="global-header">
    <div class="header-content">
      <img src="/favicon.png" alt="Logo" class="logo" /> <!-- Logo à gauche -->
      <h1>Memorial Vitor Costa</h1>
      <!-- Ajoutez ici d'autres éléments comme la navigation -->
    </div>
  </header>
</template>

<script setup>
// Composant simple de header
</script>

<style scoped>
.global-header {
  background-color: #333;
  color: white;
  padding: 10px 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.header-content {
  display: flex;
  align-items: center;
}

.logo {
  width: 50px; /* Ajustez la taille du logo selon vos préférences */
  height: auto;
  margin-right: 15px;
}

h1 {
  font-size: 1.5rem;
}
</style>
