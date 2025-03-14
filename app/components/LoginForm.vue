<template>
    <div class="pt-10 flex mx-auto items-center justify-center">
      <form @submit.prevent="seConnecter" class="mt-6 bg-white w-[60%] p-10 rounded-lg shadow-md">
        <h2 class="text-3xl font-semibold text-black text-center">Se connecter</h2>
  
        <!-- Email -->
        <div class="mb-4 relative">
          <label class="block text-black">Email <span class="text-red-500">*</span></label>
          <div class="relative">
            <span class="icon-style"><i class="ri-mail-fill"></i></span>
            <input
              type="email"
              v-model="utilisateur.email"
              class="w-full px-4 py-2 text-center border rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-500"
              required
              placeholder="Entrez votre Email"
            />
          </div>
        </div>
  
        <!-- Mot de passe -->
        <div class="mb-4 relative">
          <label class="block text-black">Mot de passe <span class="text-red-500">*</span></label>
          <div class="relative">
            <span class="icon-style"><i class="ri-lock-fill"></i></span>
            <input
              type="password"
              v-model="utilisateur.password"
              class="w-full px-4 py-2 text-center border rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-500"
              required
              placeholder="Entrez votre mot de passe"
            />
          </div>
        </div>
  
     
        <div class="mt-10 text-center">
            <BaseBtn
              content="Se connecter"
              customClass="bg-black text-white hover:bg-slate-800 px-2 rounded-md w-full"
              
            />
        </div>
  
        <div class="mt-5">
          <p class="text-black cursor-pointer text-center">
            Pas encore inscrit ?
            <NuxtLink to="/register" class="text-blue-400 hover:text-blue-700"> Créez un compte</NuxtLink>
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
    email: "",
    password: "",
  });
  
  const seConnecter = async () => {
    try {
    const {data, error}  = await useFetch("https://booking.openintech.app/api/login", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Shop-Id": "072f100a-9009-4e5c-98a2-007f2f24cf11",
        },
        body: utilisateur.value,
       
      });
  
     if(!error.value){
        localStorage.setItem("token", data.value.token)
        router.push("/");
     }
       
      
      
    } catch (error) {
      alert("Erreur de connexion. Veuillez vérifier vos informations.");
    }
  };
  </script>
  
  <style scoped>
  .icon-style {
    position: absolute;
    left: 10px;
    top: 50%;
    transform: translateY(-50%);
    color: #6b7280;
  }
  </style>
  