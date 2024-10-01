<template>
  <section class="py-12 bg-site-bg">
    <div class="container px-4 mx-auto">
      <div class="relative">
        <div class="flex overflow-x-hidden" ref="slider">
          <div class="flex w-full">
            <div
              v-for="(slide, index) in visibleSlides"
              :key="index"
              class="w-full md:w-1/3 px-2 mb-8"
            >
              <div class="h-full p-6 bg-white rounded-lg shadow-lg text-center flex flex-col justify-between">
                <div class="relative">
                  <img
                    :src="`/images/${slide.image}`"
                    :alt="'Image ' + (index + 1)"
                    class="object-cover w-full h-40 rounded-t-lg mb-4"
                  />
                  <h3
                    class="mt-4 text-lg font-semibold transition-transform duration-300 transform hover:translate-y-[-10px] relative z-10"
                  >
                    {{ slide.title }}
                  </h3>
                  <p
                    class="text-gray-600 transition-transform duration-300 transform hover:translate-y-[-5px] relative z-10"
                  >
                    {{ slide.description }}
                  </p>
                </div>
                <a
                  href="#"
                  class="inline-block px-4 py-2 mt-4 text-center text-white bg-blue-500 rounded-lg"
                >
                  Voir Plus
                </a>
              </div>
            </div>
          </div>
        </div>

        <button
          @click="prev_slide"
          class="absolute p-2 transition-all transform -translate-y-1/2 bg-yellow-500 rounded-full left-0 top-1/2 hover:bg-yellow-600"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            class="w-6 h-6 text-white"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M15 19l-7-7 7-7"
            />
          </svg>
        </button>

        <button
          @click="next_slide"
          class="absolute p-2 transition-all transform -translate-y-1/2 bg-yellow-500 rounded-full right-0 top-1/2 hover:bg-yellow-600"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            class="w-6 h-6 text-white"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M9 5l7 7-7 7"
            />
          </svg>
        </button>
      </div>
      
      <!-- Boutons de pagination -->
      <div class="flex justify-center mt-4">
        <button
          v-for="(slide, index) in slides"
          :key="index"
          @click="go_to_slide(index)"
          :class="{
            'bg-yellow-500': isMobile ? current_index === index : (index >= current_index && index < current_index + 3),
            'bg-gray-300': isMobile ? current_index !== index : (index < current_index || index >= current_index + 3)
          }"
          class="w-3 h-3 rounded-full mx-1 focus:outline-none"
        ></button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'News',
  data() {
    return {
      current_index: 0,
      isMobile: false,
      slides: [
        {
          id: 1,
          title: 'Title 1',
          description: 'The LEGS is a search-based system that allows access, retrieve, or save structured bills information and status as well as download full ram.',
          image: 'ev1.jpg',
        },
        {
          id: 2,
          title: 'Title 2',
          description: 'The LEGS is a search-based system that allows access, retrieve, or save structured bills information and status as well as download full ram.',
          image: 'ev2.jpg',
        },
        {
          id: 3,
          title: 'Title 3',
          description: 'The LEGS is a search-based system that allows access, retrieve, or save structured bills information and status as well as download full ram.',
          image: 'ev3.jpg',
        },
        {
          id: 4,
          title: 'Title 4',
          description: 'The LEGS is a search-based system that allows access, retrieve, or save structured bills information and status as well as download full ram.',
          image: 'ev4.jpg',
        },
      ],
    };
  },
  computed: {
    visibleSlides() {
      if (this.isMobile) {
        return [this.slides[this.current_index]];
      } else {
        return this.slides.slice(this.current_index, this.current_index + 3);
      }
    },
  },
  mounted() {
    this.checkViewport();
    window.addEventListener('resize', this.checkViewport);
  },
  methods: {
    next_slide() {
      const maxIndex = this.isMobile ? this.slides.length - 1 : this.slides.length - 3;
      this.current_index = (this.current_index + 1) % (maxIndex + 1);
    },
    prev_slide() {
      const maxIndex = this.isMobile ? this.slides.length - 1 : this.slides.length - 3;
      this.current_index = (this.current_index - 1 + maxIndex + 1) % (maxIndex + 1);
    },
    go_to_slide(index) {
      if (this.isMobile) {
        this.current_index = index;
      } else {
        this.current_index = Math.min(index, this.slides.length - 3);
      }
    },
    checkViewport() {
      this.isMobile = window.innerWidth < 768;
    },
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.checkViewport);
  },
};
</script>

<style scoped>
/* Styles pour le texte */
h3:hover, p:hover {
  transform: translateY(-10px); /* Monter de 10px */
}
h3, p {
  transition: transform 0.3s ease; /* Transition douce */
}
</style>
