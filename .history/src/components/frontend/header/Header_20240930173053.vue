<template>
  <header class="py-4 shadow-md bg-site-bg">
    <div class="container px-4 mx-auto">
      <div class="flex flex-col items-center justify-between p-4 transition-all duration-300 ease-in-out bg-white rounded-lg shadow-lg md:flex-row hover:shadow-xl">
        <!-- Logo et titre -->
        <div class="flex items-center mb-4 transition-transform duration-300 ease-in-out md:mb-0 hover:scale-105">
          <img src="/images/logo/logo-adna.png" alt="Logo ADNA" class="w-auto h-12 mr-3">
          <h1 class="text-lg font-bold text-yellow-700 transition-colors duration-300 ease-in-out hover:text-yellow-600">
            CONGRÈS NDOGBATJECK
          </h1>
        </div>

        <!-- Informations du congrès avec défilement centré -->
        <div class="relative flex items-center justify-center w-full h-10 mb-4 overflow-hidden md:w-auto md:mb-0">
          <div 
            class="text-center animate-scroll whitespace-nowrap" 
            style="animation-duration: 20s;"
          >
            <p class="inline-block text-sm font-semibold text-gray-700">
              📅 23 au 26 Janvier 2025
            </p>
            <span class="mx-4">|</span>
            <p class="inline-block text-xs text-gray-600">
              EKOANGOMBE SUD - MANGOG
            </p>
          </div>
        </div>

        <!-- Compte à rebours et contrôles -->
        <div class="flex flex-col items-center">
          <div class="mb-2 text-2xl font-bold text-red-600" :class="{ 'animate-pulse': isRunning }">
            {{ displayText }}
          </div>
          <div class="flex space-x-2">
            <button 
              @click="toggleCountdown" 
              class="px-4 py-2 text-sm font-semibold transition-colors duration-300 ease-in-out rounded-full"
              :class="isRunning ? 'bg-red-500 hover:bg-red-600 text-white' : 'bg-green-500 hover:bg-green-600 text-white'"
            >
              {{ isRunning ? 'Arrêter' : 'Démarrer' }}
            </button>
            <button 
              @click="resetCountdown" 
              class="px-4 py-2 text-sm font-semibold text-white transition-colors duration-300 ease-in-out bg-blue-500 rounded-full hover:bg-blue-600"
            >
              Réinitialiser
            </button>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>
<script>
import { ref, computed, onMounted, onUnmounted } from 'vue';

export default {
  name: 'AdvancedCountdownHeader',
  setup() {
    const targetDate = new Date('2025-01-23T00:00:00').getTime();
    const now = ref(Date.now());
    const isRunning = ref(true);
    const isClosed = ref(false);
    let timer;

    const timeLeft = computed(() => {
      const difference = targetDate - now.value;
      if (difference <= 0) {
        return { days: 0, hours: 0, minutes: 0, seconds: 0 };
      }
      return {
        days: Math.floor(difference / (1000 * 60 * 60 * 24)),
        hours: Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)),
        minutes: Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60)),
        seconds: Math.floor((difference % (1000 * 60)) / 1000)
      };
    });

    const displayText = computed(() => {
      if (isClosed.value) {
        return "Le congrès est fermé";
      }
      if (!isRunning.value) {
        return "Compte à rebours en pause";
      }
      const { days, hours, minutes, seconds } = timeLeft.value;
      if (days + hours + minutes + seconds <= 0) {
        return "Le congrès a commencé!";
      }
      return `${days}j ${hours}h ${minutes}m ${seconds}s`;
    });

    const updateCountdown = () => {
      if (isRunning.value && !isClosed.value) {
        now.value = Date.now();
        if (timeLeft.value.days + timeLeft.value.hours + timeLeft.value.minutes + timeLeft.value.seconds <= 0) {
          isRunning.value = false;
        }
      }
    };

    const toggleCountdown = () => {
      if (isClosed.value) {
        isClosed.value = false;
        isRunning.value = true;
      } else {
        isRunning.value = !isRunning.value;
      }
    };

    const resetCountdown = () => {
      now.value = Date.now();
      isRunning.value = true;
      isClosed.value = false;
    };

    onMounted(() => {
      timer = setInterval(updateCountdown, 1000);
    });

    onUnmounted(() => {
      clearInterval(timer);
    });

    return {
      displayText,
      isRunning,
      toggleCountdown,
      resetCountdown
    };
  }
};
</script>
<style scoped>
@keyframes scroll {
  0% {
    transform: translateX(100%);
  }
  100% {
    transform: translateX(-100%);
  }
}
.animate-scroll {
  display: inline-block;
  animation: scroll linear infinite;
}
@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}
.animate-pulse {
  animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
</style>
