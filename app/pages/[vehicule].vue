<template>
    <section class="pt-20">
    <div v-if="!$route.query.hideSearchButton" class="container max-w-full">
      <div class="shadow-lg p-[30px]">
        <div class="flex gap-3 text-center mb-4">
          <button
            class="w-full bg-black rounded-md h-12 text-white font-roboto font-[500] text-sm mt-3 cursor-pointer hover:bg-slate-800 hover:text-slate-200"
            @click="goToSearch"
          >
            Rechercher un véhicule
          </button>
        </div>
      </div>
    </div>
</section>
  </template>
  
  <script setup>
  import { useRouter } from "vue-router";
  
  
  const router = useRouter();
  
  const goToSearch = () => {
    router.push("/search");
  };
  
  </script>