<template>
  <nav class="bg-[#9C7C13] text-white py-2 relative">
    <div class="container px-4 mx-auto">
      <div class="flex items-center justify-center space-x-10">
        <!-- Always visible items -->
        <div @click="toggleSubmenu" class="nav-item cursor-pointer hover:bg-[#8b6b10] rounded-lg px-2 py-1 transition-all duration-300 relative">
          <div class="icon-circle bg-[#0056ff]">
            <img src="/images/menu/accueil.svg" alt="Accueil" class="w-6 h-6">
          </div>
          <span class="mt-1 text-xs">Accueil</span>
        </div>

        <transition name="fade">
          <div v-if="isSubmenuOpen" class="absolute z-10 w-48 mt-2 bg-white rounded-md shadow-lg bg-opacity-90 backdrop-blur-lg">
            <div class="py-1" role="none">
              <a href="#" @click="selectMenu('Mot du Chef Canton NDOGBATJECK')" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100" role="menuitem">Mot du Chef Canton NDOGBATJECK</a>
              <a href="#" @click="selectMenu('Mot du Président ADNA NDOGBATJECK')" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100" role="menuitem">Mot du Président ADNA NDOGBATJECK</a>
              <a href="#" @click="selectMenu('Présentation du Canton NDOGBATJECK')" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100" role="menuitem">Présentation du Canton NDOGBATJECK</a>
              <a href="#" @click="selectMenu('Listes des villages NDOGBATJECK')" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100" role="menuitem">Listes des villages NDOGBATJECK</a>
              <a href="#" @click="selectMenu('Listes des Associations NDOGBATJECK')" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100" role="menuitem">Listes des Associations NDOGBATJECK</a>
              <a href="#" @click="selectMenu('L’Hôte du congrès NDOGBATJECK')" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100" role="menuitem">L’Hôte du congrès NDOGBATJECK</a>
            </div>
          </div>
        </transition>

        <!-- Selected Menu Item Display -->
        <div v-if="selectedMenu" class="mt-4 text-xs text-center">
          <span class="text-white">Vous avez sélectionné: {{ selectedMenu }}</span>
        </div>

        <!-- Other items -->
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

        <!-- Other menu items -->
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

          <!-- Language selector -->
          <div class="relative flex flex-col items-center">
            <div class="icon-circle bg-[#FF6347]">
              <img src="/images/menu/langue.svg" alt="Langue" class="w-6 h-6">
            </div>
            <div class="flex items-center mt-1">
              <span class="text-xs">Traduction</span>
              <select v-model="selectedLanguage" @change="handleLanguageChange" class="ml-1 text-white bg-transparent bg-site-bg nav-select hover:bg-gray-600">
                <option value="fr">FR</option>
                <option value="en">EN</option>
              </select>
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
          <div class="mb-4 nav-item" @click="toggleSubmenu('mediatheque')">
            <div class="cursor-pointer flex flex-col items-center hover:bg-[#8b6b10] rounded-lg px-2 py-1 transition-all duration-300">
              <div class="icon-circle bg-[#DAA520]">
                <img src="/images/menu/Médiathèque.svg" alt="Médiathèque" class="w-6 h-6">
              </div>
              <span class="mt-1 text-xs">Médiathèque</span>
            </div>
          </div>
          <div class="mb-4 nav-item" @click="toggleSubmenu('hymne')">
            <div class="cursor-pointer flex flex-col items-center hover:bg-[#8b6b10] rounded-lg px-2 py-1 transition-all duration-300">
              <div class="icon-circle bg-[#FF6347]">
                <img src="/images/menu/hymne.svg" alt="Hymne" class="w-6 h-6">
              </div>
              <span class="mt-1 text-xs">Hymne</span>
            </div>
          </div>
          <div class="mb-4 nav-item">
            <div class="flex flex-col items-center">
              <div class="icon-circle bg-[#FF6347]">
                <img src="/images/menu/langue.svg" alt="Langue" class="w-6 h-6">
              </div>
              <div class="flex items-center">
                <span class="text-xs">Traduction</span>
                <select v-model="selectedLanguage" @change="handleLanguageChange" class="ml-1 text-white bg-transparent bg-site-bg nav-select hover:bg-gray-600">
                  <option value="fr">FR</option>
                  <option value="en">EN</option>
                </select>
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
      isSubmenuOpen: false,
      selectedMenu: null,
      selectedLanguage: 'fr',
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
      this.isSubmenuOpen = false;
    },
    toggleSubmenu() {
      this.isSubmenuOpen = !this.isSubmenuOpen;
      this.selectedMenu = null; // Reset selected menu when opening submenu
    },
    selectMenu(menuItem) {
      this.selectedMenu = menuItem;
      this.isSubmenuOpen = false; // Close submenu after selection
    },
    handleLanguageChange() {
      // Add your language change handling logic here
      console.log(`Language changed to: ${this.selectedLanguage}`);
    },
  },
};
</script>

<style scoped>
.nav-item {
  position: relative;
}

.icon-circle {
  border-radius: 50%;
  padding: 0.5rem;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.3s ease;
}

.slide-fade-enter, .slide-fade-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

.bg-site-bg {
  background: rgba(255, 255, 255, 0.8); /* Change this to match your desired background */
}

/* Adjust the nav styles if needed */
</style>
