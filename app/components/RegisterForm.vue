<template>
  <div class="pt-10 flex mx-auto items-center justify-center">
    <form
      @submit.prevent="soumettreFormulaire"
      class="bg-white w-[60%] p-10 rounded-lg shadow-md"
    >
      <h2 class="text-3xl font-semibold text-gray-700 text-center">
        Créer un compte
      </h2>

      <!-- Nom -->
      <div class="mb-4">
        <label class="block text-black"
          >Nom <span class="text-red-500">*</span></label
        >
        <input
          type="text"
          v-model="utilisateur.firstname"
          class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-500"
          required
          placeholder="Entrez votre nom"
        />
      </div>

      <!-- Prénom -->
      <div class="mb-4">
        <label class="block text-black">Prénom</label>
        <input
          type="text"
          v-model="utilisateur.lastname"
          class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-500"
          placeholder="Entrez votre prénom"
        />
      </div>

      <!-- Email -->
      <div class="mb-4">
        <label class="block text-black"
          >Email <span class="text-red-500">*</span></label
        >
        <input
          type="email"
          v-model="utilisateur.email"
          class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-500"
          required
          placeholder="Entrez votre Email"
        />
      </div>

      <!-- Mot de passe -->
      <div class="mb-4">
        <label class="block text-black"
          >Mot de passe <span class="text-red-500">*</span></label
        >
        <input
          type="password"
          v-model="utilisateur.password"
          class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-500"
          required
          placeholder="Entrez votre mot de passe"
        />
      </div>

      <!-- Confirmer mot de passe -->
      <div class="mb-4">
        <label class="block text-black">Confirmer votre mot de passe</label>
        <input
          type="password"
          v-model="utilisateur.password_confirmation"
          class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-500"
          placeholder="Confirmez votre mot de passe"
        />
      </div>
      <!-- Champ Téléphone -->
      <div class="mb-4">
        <label class="block text-black">Téléphone</label>

        <input
          type="tel"
          v-model="utilisateur.phone"
          class="w-full px-4 py-2 border text-center rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-500"
          placeholder="Entrez votre numéro"
        />
      </div>

      <!-- Bouton -->
      <div class="mt-10">
        <BaseBtn
          content="S'inscrire"
          customClass="bg-black text-white hover:bg-slate-800 px-2 rounded-md w-full"
        />
      </div>

      <div class="mt-5">
        <p class="text-black cursor-pointer text-center">
          Déjà un compte ?
          <NuxtLink to="/login" class="text-blue-400 hover:text-blue-700">
            Connectez-vous</NuxtLink
          >
        </p>
      </div>
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
const utilisateur = ref({
  firstname: "",
  lastname: "",
  email: "",
  password: "",
  password_confirmation: "",
});

const soumettreFormulaire = async () => {
  try {
    const { data, error } = await useFetch(
      "https://booking.openintech.app/api/register",
      {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Shop-Id": "072f100a-9009-4e5c-98a2-007f2f24cf11",
        },
        body: utilisateur.value,
      }
    );
    if (!error.value) {
      localStorage.setItem("token", data.value.token);
      alert("Inscription réussie !");
      router.push("/login");
    } else {
      alert("Erreur de connexion. Veuillez vérifier vos informations.");
    }
  } catch (error) {
    alert("Erreur lors de l'inscription.");
  }
};
</script>
