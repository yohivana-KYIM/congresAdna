<template>
  <nav class="bg-[#9C7C13] text-white py-2">
    <div class="container px-4 mx-auto">
      <div class="flex items-center justify-center space-x-10">
        <!-- Always visible items -->
        <div @click="toggleSubmenu('accueil')" class="nav-item cursor-pointer hover:bg-[#8b6b10] rounded-lg px-2 py-1 transition-all duration-300">
          <div class="icon-circle bg-[#0056ff]">
            <img src="/images/menu/accueil.svg" alt="Accueil" class="w-6 h-6">
          </div>
          <span class="mt-1 text-xs">Accueil</span>
        </div>

        <!-- Submenu for Accueil -->
        <transition name="slide-fade">
          <div v-if="openSubmenu === 'accueil'" class="bg-[#9C7C13] mt-2 rounded-lg shadow-lg p-2">
            <a href="#" class="block py-2 hover:bg-[#8b6b10] rounded">Mot du Chef Canton NDOGBATJECK</a>
            <a href="#" class="block py-2 hover:bg-[#8b6b10] rounded">Mot du Président ADNA NDOGBATJECK</a>
            <a href="#" class="block py-2 hover:bg-[#8b6b10] rounded">Présentation du Canton NDOGBATJECK</a>
            <a href="#" class="block py-2 hover:bg-[#8b6b10] rounded">Listes des villages NDOGBATJECK</a>
            <a href="#" class="block py-2 hover:bg-[#8b6b10] rounded">Listes des Associations NDOGBATJECK</a>
            <a href="#" class="block py-2 hover:bg-[#8b6b10] rounded">L’Hôte du congrès NDOGBATJECK</a>
          </div>
        </transition>

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
