<template>
  <section class="p-4 bg-gray-100 overflow-hidden">
    <div class="container mx-auto px-4 md:px-6">
      <div class="relative">
        <div class="scroll-container flex justify-center"> <!-- Ajout de justify-center -->
          <div v-for="n in 5" :key="n" class="flex items-center space-x-4 md:space-x-6 animate-scroll">
            <div v-for="(partner, index) in partners" :key="`${n}-${index}`" class="flex-shrink-0 w-10 h-10 md:w-16 md:h-16 rounded-full overflow-hidden bg-white flex items-center justify-center shadow-lg"> <!-- Ajout de shadow-lg pour une meilleure visibilité -->
              <img :src="partner.logo" :alt="partner.name" class="max-h-8 max-w-8 md:max-h-12 md:max-w-12 object-contain" @error="handleImageError">
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import partner1 from '@/assets/partner1.png';
import partner2 from '@/assets/partner2.png';
import partner3 from '@/assets/partner3.png';

export default {
  name: 'Partners',
  data() {
    return {
      partners: [
        { name: 'Partner 1', logo: partner1 },
        { name: 'Partner 2', logo: partner2 },
        { name: 'Partner 3', logo: partner3 }
      ]
    }
  },
  methods: {
    handleImageError(event) {
      event.target.src = '/images/default-partner.png'; // Chemin vers une image par défaut
    }
  }
}
</script>

<style scoped>
.scroll-container {
  width: 120%; /* Réduit encore la largeur totale de la zone défilante */
  display: flex;
  overflow: hidden;
}

.animate-scroll {
  animation: scroll 10s linear infinite; /* Réduit la durée de l'animation */
}

@keyframes scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

/* Pause animation on hover */
.scroll-container:hover .animate-scroll {
  animation-play-state: paused;
}

/* Ajustement pour les écrans plus petits */
@media (max-width: 768px) {
  .animate-scroll {
    animation-duration: 8s; /* Animation plus rapide sur mobile */
  }
}
</style>
