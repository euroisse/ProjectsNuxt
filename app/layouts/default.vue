<template>
   <div class="relative h-max w-screen overflow-x-hidden">
    <BaseNavigation 
    :isAuthenticated="isAuthenticated" @logout="handleLogout"
   />
    <slot />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

const isAuthenticated = ref(false);

const checkAuthStatus = () => {
  isAuthenticated.value = !!localStorage.getItem('token'); // Vérifie si un token est stocké
};

const handleLogout = () => {
  localStorage.removeItem('token');
  isAuthenticated.value = false;
  console.log('Déconnexion réussie');
};


onMounted(checkAuthStatus);
</script>


<style scoped></style>
