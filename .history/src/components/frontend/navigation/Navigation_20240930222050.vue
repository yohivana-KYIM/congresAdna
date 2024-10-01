<template>
  <nav class="bg-[#9C7C13] text-white py-2">
    <div class="container px-4 mx-auto">
      <div class="flex items-center justify-center space-x-10">
        <!-- Always visible items -->
        <a href="#" class="nav-item hover:bg-[#8b6b10] rounded-lg px-2 py-1 transition-all duration-300">
          <div class="icon-circle bg-[#0056ff]">
            <img src="/images/menu/accueil.svg" alt="Accueil" class="w-6 h-6">
          </div>
          <span class="mt-1 text-xs">Accueil</span>
        </a>
        <div @click="toggleSubmenu('congres')" class="nav-item cursor-pointer hover:bg-[#8b6b10] rounded-lg px-2 py-1 transition-all duration-300">
          <div class="icon-circle bg-[#856230]">
            <img src="/images/menu/congres.svg" alt="Congrès" class="w-6 h-6">
          </div>
          <span class="mt-1 text-xs">Congrès</span>
        </div>
        <div @click="toggleSubmenu('participer')" class="nav-item cursor-pointer hover:bg-[#8b6b10] rounded-lg px-2 py-1 transition-all duration-300">
          <div class="icon-circle bg-[#32CD32]">
            <img src="/images/menu/participer.svg" alt="Participer" class="w-6 h-6">
          </div>
          <span class="mt-1 text-xs">Participer</span>
        </div>

        <!-- Desktop menu items -->
        <div class="items-center hidden space-x-4 md:flex">
          <div @click="toggleSubmenu('mediatheque')" class="cursor-pointer flex flex-col items-center hover:bg-[#8b6b10] rounded-lg px-2 py-1 transition-all duration-300">
            <div class="icon-circle bg-[#DAA520]">
              <img src="/images/menu/Médiathèque.svg" alt="Médiathèque" class="w-6 h-6">
            </div>
            <span class="mt-1 text-xs">Médiathèque</span>
          </div>
          <div @click="toggleSubmenu('hymne')" class="cursor-pointer flex flex-col items-center hover:bg-[#8b6b10] rounded-lg px-2 py-1 transition-all duration-300">
            <div class="icon-circle bg-[#FF6347]">
              <img src="/images/menu/hymne.svg" alt="Hymne" class="w-6 h-6">
            </div>
            <span class="mt-1 text-xs">Hymne</span>
          </div>

          <!-- Language selector with icon and aligned text -->
          <div class="relative flex flex-col items-center">
            <div class="icon-circle bg-[#FF6347]">
              <img src="/images/menu/langue.svg" alt="Langue" class="w-6 h-6">
            </div>
            <span class="text-xs">Traduction</span>
            <button @click="toggleDropdown" class="nav-select text-white bg-gray-700 hover:bg-gray-600 mt-1">
              {{ selectedLanguage }} ▼
            </button>
            <div v-if="dropdownOpen" class="absolute left-0 mt-2 w-full bg-gray-800 rounded shadow-lg z-10">
              <button @click="changeLanguage('fr')" class="block px-4 py-2 text-sm text-white hover:bg-gray-700 w-full text-left">FR</button>
              <button @click="changeLanguage('en')" class="block px-4 py-2 text-sm text-white hover:bg-gray-700 w-full text-left">EN</button>
            </div>
          </div>
        </div>

        <!-- Hamburger menu for mobile -->
        <button @click="toggleMenu" class="text-white md:hidden focus:outline-none">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path>
          </svg>
        </button>
      </div>

      <!-- Mobile menu -->
      <transition name="slide-fade">
        <div v-if="isMenuOpen" class="mt-4 md:hidden">
          <div class="mb-4 nav-item">
            <div @click="toggleSubmenu('mediatheque')" class="cursor-pointer flex flex-col items-center hover:bg-[#8b6b10] rounded-lg px-2 py-1 transition-all duration-300">
              <div class="icon-circle bg-[#DAA520]">
                <img src="/images/menu/Médiathèque.svg" alt="Médiathèque" class="w-6 h-6">
              </div>
              <span class="mt-1 text-xs">Médiathèque</span>
            </div>
          </div>
          <div class="mb-4 nav-item">
            <div @click="toggleSubmenu('hymne')" class="cursor-pointer flex flex-col items-center hover:bg-[#8b6b10] rounded-lg px-2 py-1 transition-all duration-300">
              <div class="icon-circle bg-[#FF6347]">
                <img src="/images/menu/hymne.svg" alt="Hymne" class="w-6 h-6">
              </div>
              <span class="mt-1 text-xs">Hymne</span>
            </div>
          </div>
          <div class="mb-4 nav-item">
            <div class="relative flex flex-col items-center">
              <div class="icon-circle bg-[#FF6347]">
                <img src="/images/menu/langue.svg" alt="Langue" class="w-6 h-6">
              </div>
              <span class="text-xs">Traduction</span>
              <button @click="toggleDropdown" class="nav-select text-white bg-gray-700 hover:bg-gray-600 mt-1">
                {{ selectedLanguage }} ▼
              </button>
              <div v-if="dropdownOpen" class="absolute left-0 mt-2 w-full bg-gray-800 rounded shadow-lg z-10">
                <button @click="changeLanguage('fr')" class="block px-4 py-2 text-sm text-white hover:bg-gray-700 w-full text-left">FR</button>
                <button @click="changeLanguage('en')" class="block px-4 py-2 text-sm text-white hover:bg-gray-700 w-full text-left">EN</button>
              </div>
            </div>
          </div>
        </div>
      </transition>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      isMenuOpen: false,
      openSubmenu: null,
      dropdownOpen: false,
      selectedLanguage: 'FR',
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
      this.openSubmenu = null;
    },
    toggleSubmenu(submenu) {
      this.openSubmenu = this.openSubmenu === submenu ? null : submenu;
    },
    toggleDropdown() {
      this.dropdownOpen = !this.dropdownOpen;
    },
    changeLanguage(language) {
      this.selectedLanguage = language === 'fr' ? 'FR' : 'EN';
      this.dropdownOpen = false; // Close dropdown after selection
      console.log('Langue sélectionnée:', this.selectedLanguage);
    },
  },
};
</script>

<style scoped>
.nav-item {
  @apply flex flex-col items-center justify-center w-auto;
  margin-left: 10px;
}

.icon-circle {
  @apply flex items-center justify-center bg-white rounded-full w-10 h-10;
}

.nav-select {
  @apply bg-[#9C7C13] text-white py-1 px-2 rounded appearance-none w-full text-center text-xs sm:text-sm;
}

img {
  @apply h-6 w-6;
}
</style>
