<template>
  <nav
    v-if="showHeader"
    class="flex items-center shadow-sm w-full justify-between h-16 sm:h-20 fixed z-50 top-0 duration-300 bg-white"
  >
    <div class="container flex items-center justify-between">
      <div>
        <NuxtLink to="/">
          <NuxtImg src="/nuxt-icon.png" width="32px" />
        </NuxtLink>
      </div>

      <div
        :class="[
          isMenuOpen ? 'left-0' : 'left-[-100%]',
          'absolute top-0 min-h-[80vh] w-full bg-white backdrop-blur-sm flex flex-col items-center justify-center gap-8 duration-300 overflow-hidden',
          'lg:static lg:min-h-fit lg:bg-transparent lg:w-auto lg:flex lg:flex-row lg:opacity-100 lg:left-auto',
        ]"
      >
        <ul class="flex flex-col items-center gap-8 lg:flex-row text-[#6B7280]">
          <li v-for="(link, index) in navLinks" :key="index">
            <NuxtLink
              :to="link.to"
              :class="{
                'bg-white shadow-lg border-b-2 border-black text-black hover:text-black':
                  route.path === link.to,
                'bg-white border-none hover:text-black': route.path !== link.to,
              }"
              @click="handleClick(link.to)"
            >
              {{ link.text }}
            </NuxtLink>
          </li>
        </ul>
      </div>

      <!-- Boutons Authentification -->
      <div class="flex flex-row items-center gap-2 flex-wrap md:hidden lg:flex">
        <template v-if="!isAuthenticated">
          <BaseBtn
            content="Se connecter"
            customClass="bg-black text-white hover:bg-slate-800 px-2 rounded-md"
            @click="openLogin"
          />
          <BaseBtn
            content="S'inscrire"
            customClass="bg-white text-black border border-black hover:bg-gray-800 hover:text-white px-2"
            @click="openRegister"
          />
        </template>
        <template v-else>
          <BaseBtn
            content="Se déconnecter"
            customClass="bg-black text-white hover:bg-slate-800 px-2 rounded-md"
            @click="logout"
          />
        </template>
      </div>

      <!-- Menu Mobile -->
      <div
        class="text-xl sm:text-3xl cursor-pointer z-50 lg:hidden"
        @click="toggleMenu"
      >
        <i
          :class="
            isMenuOpen
              ? 'ri-close-line text-[#6B7280]'
              : 'ri-menu-line text-[#6B7280]'
          "
        >
        </i>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, computed } from "vue";
import { useRoute, useRouter } from "nuxt/app";

const router = useRouter();
const route = useRoute();
const isMenuOpen = ref(false);

defineEmits(["logout"]);
defineProps({ isAuthenticated: Boolean });

const navLinks = ref([
  { text: "Accueil", to: "/" },
  { text: "Véhicules", to: "/vehicles" },
  { text: "Services", to: "/services" },
  { text: "Contact", to: "/contact" },
]);

const openRegister = () => {
  router.push("/register");
};

const openLogin = () => {
  router.push("/login");
};

const logout = async () => {
  try {
    await useFetch("https://booking.openintech.app/api/logout", {
      method: "POST",
      headers: {
        Authorization: `Bearer ${localStorage.getItem("token")}`,
        "Shop-Id": "072f100a-9009-4e5c-98a2-007f2f24cf11",
        "Content-Type": "application/json",
      },
    });

    localStorage.removeItem("token");
    isAuthenticated.value = false; // Mettre à jour l'état
    router.push("/");
  } catch (error) {
    console.error("Erreur de déconnexion", error);
  }
};

const showHeader = computed(
  () => !["/login", "/register"].includes(route.path)
);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const handleClick = () => {
  if (window.innerWidth < 1024) {
    isMenuOpen.value = false;
  }
};
</script>
