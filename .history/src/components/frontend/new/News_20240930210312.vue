<template>
  <section class="container mx-auto px-4 py-12 md:py-16 lg:py-20">
    <h2 class="mb-8 text-4xl font-bold text-center text-gray-800 md:text-5xl lg:text-6xl">Blog du Congrès ADNA</h2>

    <div class="grid grid-cols-1 gap-6 overflow-hidden rounded-lg md:grid-cols-2 lg:grid-cols-3">
      <article 
        v-for="(post, index) in displayedPosts" 
        :key="post.id" 
        class="overflow-hidden transition-all duration-300 hover:shadow-lg rounded-xl bg-white"
      >
        <div class="relative group">
          <img 
            :src="post.image" 
            alt="Image de l'article" 
            loading="lazy"
            class="object-cover w-full h-48 transition-transform duration-300 transform cursor-pointer group-hover:scale-105"
          >
        </div>
        <div class="p-6">
          <h3 
            class="text-2xl font-bold text-primary mb-4 transition-all duration-300 transform group-hover:-translate-y-1"
          >
            {{ post.title }}
          </h3>
          <p 
            class="text-gray-600 mb-6 transition-all duration-300 transform group-hover:translate-x-1"
          >
            {{ post.excerpt }}
          </p>
          <router-link 
            :to="`/blog/${post.id}`" 
            class="inline-block px-6 py-2 text-white bg-blue-500 hover:bg-blue-700 rounded-full transition-colors duration-200"
          >
            Lire la suite
          </router-link>
        </div>
      </article>
    </div>

    <div class="mt-12 flex justify-center space-x-4">
      <button 
        @click="previousView" 
        aria-label="Vue précédente"
        class="w-10 h-10 flex items-center justify-center text-gray-800 transition-all duration-200 transform rounded-full bg-transparent hover:bg-gray-100"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
        </svg>
      </button>
      <div class="flex items-center">
        <span 
          v-for="(page, index) in visiblePageNumbers" 
          :key="index" 
          @click="goToView(page)" 
          class="px-4 py-2 mx-2 text-sm text-gray-600 cursor-pointer hover:text-primary transition-colors duration-200"
        >
          {{ page }}
        </span>
      </div>
      <button 
        @click="nextView" 
        aria-label="Vue suivante"
        class="w-10 h-10 flex items-center justify-center text-gray-800 transition-all duration-200 transform rounded-full bg-transparent hover:bg-gray-100"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
        </svg>
      </button>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      posts: [
        {
          id: 1,
          title: 'Bienvenue au Congrès ADNA 2024',
          excerpt: 'Découvrez les dernières informations et mises à jour sur le congrès ADNA de cette année.',
          image: '/images/blog/ev1.jpg',
        },
        {
          id: 2,
          title: 'Conférenciers et Thèmes',
          excerpt: 'Rencontrez nos conférenciers invités et explorez les thèmes qui seront abordés.',
          image: '/images/blog/ev2.jpg',
        },
        {
          id: 3,
          title: 'Inscription et Tarification',
          excerpt: 'Tous les détails concernant l\'inscription au congrès et les options de tarification.',
          image: '/images/blog/ev3.jpg',
        },
        {
          id: 4,
          title: 'Ateliers Pratiques',
          excerpt: 'Participez à nos ateliers interactifs et apprenez des experts.',
          image: '/images/blog/ev4.jpg',
        },
        {
          id: 5,
          title: 'Networking et Échanges',
          excerpt: 'Rencontrez d\'autres participants et établissez des contacts.',
          image: '/images/blog/ev5.jpg',
        },
        {
          id: 6,
          title: 'Clôture du Congrès',
          excerpt: 'Revivez les moments forts du congrès ADNA.',
          image: '/images/blog/ev6.jpg',
        },
      ],
      visibleSlides: 3, // Nombre de slides affichées simultanément
      currentView: 1, // Vue actuelle
      totalViews: Math.ceil(this.posts.length / this.visibleSlides), // Total de vues possibles
    };
  },
  computed: {
    displayedPosts() {
      const start = (this.currentView - 1) * this.visibleSlides;
      return this.posts.slice(start, start + this.visibleSlides);
    },
    visiblePageNumbers() {
      const pageNumbers = [];
      for (let i = 1; i <= this.totalViews; i++) {
        if (i === 1 || i === this.totalViews || (i > this.currentView - 1 && i < this.currentView + 2)) {
          pageNumbers.push(i);
        }
      }
      return pageNumbers;
    },
    isLastView() {
      return this.currentView >= this.totalViews;
    },
    isFirstView() {
      return this.currentView === 1;
    },
  },
  methods: {
    nextView() {
      if (!this.isLastView) {
        this.currentView++;
      }
    },
    previousView() {
      if (!this.isFirstView) {
        this.currentView--;
      }
    },
    goToView(page) {
      this.currentView = page;
    },
  },
};
</script>

<style scoped>
/* Ajoutez ici des styles spécifiques si nécessaire */
</style>
