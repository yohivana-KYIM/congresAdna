<template>
  <div class="relative flex flex-col items-center justify-center min-h-screen overflow-hidden bg-gradient-to-br from-blue-900 to-yellow-700">
    <!-- Effet d'animation d'arrière-plan -->
    <div class="absolute inset-0 bg-gradient-to-r from-yellow-600 via-yellow-500 to-yellow-400 opacity-20 animate-gradient-xy"></div>

    <!-- Conteneur principal -->
    <div class="relative z-10 flex flex-col items-center p-8 transition-all duration-500 bg-black bg-opacity-50 shadow-2xl rounded-2xl backdrop-blur-md hover:bg-opacity-60">
      <h1 class="mb-6 text-5xl font-extrabold text-white drop-shadow-lg animate-title">
        Hymne National du Cameroun
      </h1>

      <!-- Paroles de l'hymne -->
      <div class="max-w-2xl p-6 mx-auto overflow-y-auto transition-all duration-500 bg-yellow-900 shadow-inner bg-opacity-30 rounded-xl backdrop-blur-sm max-h-96 hover:bg-opacity-40">
        <p
          v-for="(line, index) in hymnLyrics"
          :key="index"
          class="my-2 text-2xl leading-relaxed text-white opacity-90 animate-fadeIn"
          :style="{ animationDelay: `${index * 200}ms` }"
        >
          {{ line }}
        </p>
      </div>

      <!-- Contrôles audio -->
      <div class="flex items-center mt-10 space-x-4">
        <button
          @click="togglePlayPause"
          class="flex items-center justify-center px-6 py-3 font-bold text-white transition-all duration-300 transform bg-yellow-600 rounded-full shadow-lg group hover:bg-yellow-500 hover:scale-105 active:scale-95 focus:outline-none"
        >
          <span class="mr-2 text-3xl">
            <svg v-if="isPlaying" xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" viewBox="0 0 20 20" fill="currentColor">
              <path fillRule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zM7 8a1 1 0 012 0v4a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v4a1 1 0 102 0V8a1 1 0 00-1-1z" clipRule="evenodd" />
            </svg>
            <svg v-else xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" viewBox="0 0 20 20" fill="currentColor">
              <path fillRule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z" clipRule="evenodd" />
            </svg>
          </span>
          <span class="text-lg">{{ isPlaying ? "Pause" : "Jouer" }}</span>
        </button>
        
        <div class="text-xl text-white">
          {{ formatTime(currentTime) }} / {{ formatTime(duration) }}
        </div>
      </div>

      <!-- Barre de progression -->
      <div class="w-full max-w-md mt-4 bg-gray-200 rounded-full h-2.5 dark:bg-gray-700 overflow-hidden">
        <div
          class="bg-yellow-600 h-2.5 rounded-full transition-all duration-300 ease-out"
          :style="{ width: `${(currentTime / duration) * 100}%` }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const audio = ref(new Audio('/audio/hymne.mp3'));
const isPlaying = ref(false);
const currentTime = ref(0);
const duration = ref(0);

const hymnLyrics = [
  "Ô Cameroun berceau de nos ancêtres,",
  "Va debout et jaloux de ta liberté.",
  "Comme un soleil ton drapeau fier doit être,",
  "Un symbole ardent de foi et d'unité.",
  "Que tous tes enfants du Nord au Sud,",
  "De l'Est à l'Ouest soient tout amour !",
  "Te servir que ce soit leur seul but,",
  "Pour remplir leur devoir toujours.",
];

const togglePlayPause = () => {
  if (isPlaying.value) {
    audio.value.pause();
  } else {
    audio.value.play();
  }
  isPlaying.value = !isPlaying.value;
};

const formatTime = (time) => {
  const minutes = Math.floor(time / 60);
  const seconds = Math.floor(time % 60);
  return `${minutes}:${seconds.toString().padStart(2, '0')}`;
};

const updateTime = () => {
  currentTime.value = audio.value.currentTime;
  duration.value = audio.value.duration;
};

onMounted(() => {
  audio.value.addEventListener('timeupdate', updateTime);
  audio.value.addEventListener('loadedmetadata', () => {
    duration.value = audio.value.duration;
  });
});

onUnmounted(() => {
  audio.value.removeEventListener('timeupdate', updateTime);
  audio.value.pause();
});
</script>

<style scoped>
@keyframes gradient-xy {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

.animate-gradient-xy {
  background-size: 200% 200%;
  animation: gradient-xy 15s ease infinite;
}

@keyframes title {
  0% { opacity: 0; transform: translateY(-20px); }
  100% { opacity: 1; transform: translateY(0); }
}

.animate-title {
  animation: title 1.5s ease-out;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

.animate-fadeIn {
  animation: fadeIn 0.8s ease-out forwards;
}
</style>