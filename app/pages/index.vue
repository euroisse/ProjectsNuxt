<template>
  <section
    class="sectionHome relative pt-10 bg-cover bg-center h-screen w-full flex items-center"
  >
    <div class="container text-white">
      <div v-if="utilisateur" class="space-y-7">
        <p class="text-3xl">
          <span class="font-bold text-5xl"> Bienvenue </span>
          {{ utilisateur.firstname }},
        </p>
        <p class="text-lg text-gray-300">
          Découvrez une sélection de véhicules haut de gamme pour tous vos
          déplacements
        </p>
      </div>
      <div v-else>
        <div class="max-w-3xl space-y-7">
          <h1 class="text-5xl font-bold">Location de voitures premium</h1>
          <p class="text-lg text-gray-300">
            Découvrez une sélection de véhicules haut de gamme pour tous vos
            déplacements
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const utilisateur = ref(null);


onMounted(async()=>{
    const token = localStorage.getItem("token")
    const { data, error } = await useFetch(
      "https://booking.openintech.app/api/user",{
        headers: {
          "Content-Type": "application/json",
          "Shop-Id": "072f100a-9009-4e5c-98a2-007f2f24cf11",
          "Authorization": `Bearer ${token}`
        },
      }
    );
    if (!error.value) {

      utilisateur.value = data.value;
    } else {
      console.error("Erreur de récupération des infos utilisateur :", error.value);
    }
})
</script>

<style scoped>
.sectionHome {
  background-image: url("/nuxt-voiture1.png");
}
</style>
