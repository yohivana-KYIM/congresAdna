<template>
    <br />
    <Separator />
    <br />
    <div class="min-h-screen flex flex-col items-center justify-center bg-gradient-to-br from-[#1e3a8a] to-[#9C7C13] relative overflow-hidden">
      <!-- Effet d'animation d'arrière-plan en dégradé -->
      <div class="absolute inset-0 bg-gradient-to-r from-[#856230] via-[#DAA520] to-[#C09313] opacity-20 animate-gradient-xy"></div>
  
      <!-- Conteneur principal de l'hymne avec un effet de fond transparent -->
      <div class="relative z-10 flex flex-col items-center p-8 bg-[#00000080] rounded-lg shadow-lg">
        <h1 class="mb-6 text-5xl font-extrabold tracking-wider text-white drop-shadow-lg animate-fadeInDown">
          Hymne National
        </h1>
  
        <!-- Paroles de l'hymne avec un défilement élégant -->
        <div class="max-w-2xl mx-auto bg-[#85623090] rounded-xl shadow-inner p-6 backdrop-filter backdrop-blur-md overflow-y-auto max-h-96 transition-opacity duration-1000 animate-fadeIn delay-500">
          <p
            v-for="(line, index) in hymnLyrics"
            :key="index"
            class="text-2xl text-white leading-relaxed my-2 opacity-90 animate-slideUp delay-[index*300]"
          >
            {{ line }}
          </p>
        </div>
  
        <!-- Bouton de lecture/pause avec icône et effet d'interaction 3D -->
        <div class="mt-10">
          <button
            @click="togglePlayPause"
            class="group bg-[#DAA520] hover:bg-[#C09313] text-white font-bold py-3 px-6 rounded-full transition-all duration-300 transform hover:scale-105 active:scale-95 shadow-lg focus:outline-none flex items-center justify-center gap-3"
          >
            <span
              v-if="isPlaying"
              class="text-3xl material-icons animate-spin"
              >pause_circle_filled</span
            >
            <span
              v-else
              class="text-3xl material-icons animate-bounce"
              >play_circle_filled</span
            >
            <span class="text-lg">{{ isPlaying ? "Pause" : "Reprendre" }} le chant</span>
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import Separator from "@/components/frontend/separator/Separator.vue";
  export default {
    name: "Hynme",
    components: {
      Separator,
    },
    data() {
      return {
        audio: new Audio("/audio/hymne.mp3"), // Chemin vers votre fichier audio
        isPlaying: true,
        hymnLyrics: [
          "Ô Cameroun berceau de nos ancêtres,",
          "Va debout et jaloux de ta liberté.",
          "Comme un soleil ton drapeau fier doit être,",
          "Un symbole ardent de foi et d’unité.",
          "Que tous tes enfants du Nord au Sud,",
          "De l’Est à l’Ouest soient tout amour !",
          "Te servir que ce soit leur seul but,",
          "Pour remplir leur devoir toujours.",
        ],
      };
    },
    methods: {
      togglePlayPause() {
        if (this.isPlaying) {
          this.audio.pause();
        } else {
          this.audio.play();
        }
        this.isPlaying = !this.isPlaying;
      },
    },
    mounted() {
      this.audio.play();
      this.audio.loop = true;
    },
    beforeUnmount() {
      this.audio.pause();
    },
  };
  </script>
  
  <style scoped>
  @keyframes fadeInDown {
    0% {
      opacity: 0;
      transform: translateY(-20px);
    }
    100% {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
  
  @keyframes slideUp {
    from {
      opacity: 0;
      transform: translateY(40px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  @keyframes gradient-xy {
    0%, 100% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
  }
  
  .animate-fadeInDown {
    animation: fadeInDown 1.2s ease-out;
  }
  
  .animate-fadeIn {
    animation: fadeIn 2s ease-in-out;
  }
  
  .animate-slideUp {
    animation: slideUp 1.5s ease-out forwards;
  }
  
  .animate-gradient-xy {
    background-size: 200% 200%;
    animation: gradient-xy 5s ease infinite;
  }
  </style>
  