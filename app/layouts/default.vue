<template>
   <div class="relative h-max w-screen overflow-x-hidden">
    <BaseNavigation 
    :isAuthenticated="isAuthenticated" @logout="handleLogout"
   />
   
    <slot />
  </div>
</template>

<script setup lang="ts">

const isAuthenticated = ref(false)


const handleLogout = () => {
  isAuthenticated.value = false
  console.log('deconnexion reussie')
}
</script>

<style scoped></style>
