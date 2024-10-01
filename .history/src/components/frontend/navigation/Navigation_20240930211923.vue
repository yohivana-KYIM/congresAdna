<template>
  <nav class="bg-[#9C7C13]  text-white py-2">
    <div class="container mx-auto px-4">
      <div class="flex justify-center items-center">
        <div class="flex items-center space-x-6">
          <a href="#" class="flex flex-col items-center hover:text-gray-200">
            <img src="/images/menu/accueil.svg" alt="Accueil" class="h-8 w-8">
            <span>Accueil</span>
          </a>
          <a href="#" class="flex flex-col items-center hover:text-gray-200">
            <img src="/images/menu/congres.svg" alt="Congrès" class="h-8 w-8">
            <span>Congrès</span>
          </a>
          <div class="flex flex-col items-center hover:text-gray-200">
            <img src="/images/menu/participer.svg" alt="Participer au congrès" class="h-8 w-8">
            <a href="#" class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded mt-2">Participer au congrès</a>
          </div>
          <a href="#" class="flex flex-col items-center hover:text-gray-200">
            <img src="" alt="Médiathèque" class="h-8 w-8">
            <span>Médiathèque</span>
          </a>
          <a href="#" class="flex flex-col items-center hover:text-gray-200">
            <img src="/images/menu/hymne.svg" alt="Hymne" class="h-8 w-8">
            <span>Hymne</span>
          </a>
          <div class="flex items-center space-x-2">
            <select class="bg-gray-700 text-white py-2 px-4 rounded">
              <option value="fr">FR</option>
              <option value="en">EN</option>
            </select>
          </div>
        </div>
        <button @click="toggleMenu" class="md:hidden">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
          </svg>
        </button>
      </div>
      <div :class="{'hidden': !isMenuOpen, 'block': isMenuOpen}" class="md:flex md:items-center md:w-auto w-full mt-2 md:mt-0">
        <!-- Mobile Menu Content -->
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      isMenuOpen: false
    }
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    }
  }
}
</script>