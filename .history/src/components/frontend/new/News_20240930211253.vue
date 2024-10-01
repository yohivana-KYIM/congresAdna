<template>
  <section class="max-w-6xl py-10 mx-auto">
    <h2 class="mb-6 text-3xl font-bold text-center text-gray-800">Blog du Congrès ADNA</h2>
    
    <!-- Navigation controls -->
    <div class="flex items-center justify-between mb-4">
      <button @click="prevSlide" class="px-4 py-2 text-gray-600 bg-gray-100 rounded-full hover:bg-gray-200 focus:outline-none focus:ring-2 focus:ring-blue-500">
        Précédent
      </button>
      
      <button @click="nextSlide" class="px-4 py-2 text-white bg-blue-500 rounded-full hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-500">
        Suivant
      </button>
    </div>
    
    <!-- Pagination dots -->
    <div class="flex justify-center mt-4 space-x-2">
      <span v-for="(dot, index) in dots" :key="index" 
            :class="{'bg-blue-500': index === currentSlide}" 
            class="w-2 h-2 transition-colors duration-200 rounded-full cursor-pointer hover:bg-blue-600"></span>
    </div>
    
    <div class="grid grid-cols-1 gap-6 overflow-hidden rounded-lg md:grid-cols-2 lg:grid-cols-3">
      <article 
        v-for="post in posts" 
        :key="post.id" 
        class="overflow-hidden transition duration-300 bg-white rounded-lg shadow-md hover:bg-green-200 hover:shadow-lg"
      >
        <div class="relative group">
          <img 
            :src="post.image" 
            alt="Image de l'article" 
            class="object-cover w-full h-48 transition-transform duration-300 transform cursor-pointer group-hover:scale-110"
          >
        </div>
        <div class="p-4">
          <h3 
            class="mb-2 text-xl font-semibold text-gray-900 transition-transform duration-300 transform group-hover:translate-y-2"
          >
            {{ post.title }}
          </h3>
          <p 
            class="mb-4 text-gray-700 transition-transform duration-300 transform group-hover:-translate-y-1"
          >
            {{ post.excerpt }}
          </p>
          <router-link 
            :to="`/blog/${post.id}`" 
            class="inline-block text-blue-500 transition-colors duration-200 hover:text-blue-700"
          >
            Lire la suite
          </router-link>
        </div>
      </article>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      posts: [
        {id: 1, title: 'Bienvenue au Congrès ADNA 2024', excerpt: 'Découvrez les dernières informations et mises à jour sur le congrès ADNA de cette année.', image: '/images/blog/ev1.jpg'},
        {id: 2, title: 'Conférenciers et Thèmes', excerpt: 'Rencontrez nos conférenciers invités et explorez les thèmes qui seront abordés.', image: '/images/blog/ev2.jpg'},
        {id: 3, title: 'Inscription et Tarification', excerpt: 'Tous les détails concernant l\'inscription au congrès et les options de tarification.', image: '/images/blog/ev3.jpg'}
      ],
      currentSlide: 0,
      dots: Array(3).fill(false)
    }
  },
  methods: {
    prevSlide() {
      if (this.currentSlide > 0) {
        this.currentSlide--;
      } else {
        this.currentSlide = this.posts.length - 1;
      }
      this.updateDots();
    },
    nextSlide() {
      if (this.currentSlide < this.posts.length - 1) {
        this.currentSlide++;
      } else {
        this.currentSlide = 0;
      }
      this.updateDots();
    },
    updateDots() {
      this.dots.fill(false);
      this.dots[this.currentSlide] = true;
    }
  }
}
</script>

<style scoped>
/* Custom styles for the navigation controls */
.navigation-controls {
  @apply flex justify-between items-center mb-4;
}

.navigation-button {
  @apply px-4 py-2 rounded-full focus:outline-none focus:ring-2 focus:ring-blue-500;
}

.navigation-button:hover {
  @apply bg-opacity-80;
}

.navigation-button:focus {
  @apply ring-offset-2 ring-offset-white;
}

.pagination-dots {
  @apply flex justify-center space-x-2 mt-4;
}

.pagination-dot {
  @apply w-2 h-2 rounded-full cursor-pointer hover:bg-opacity-80 transition-colors duration-200;
}

.pagination-dot:hover {
  @apply bg-opacity-80;
}

.pagination-dot:focus {
  @apply outline-none;
}
</style>
