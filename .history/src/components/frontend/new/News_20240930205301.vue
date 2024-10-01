<template>
  <section class="max-w-6xl py-10 mx-auto">
    <h2 class="mb-6 text-3xl font-bold text-center text-gray-800">Blog du Congrès ADNA</h2>
    <div class="grid grid-cols-1 gap-6 overflow-hidden rounded-lg md:grid-cols-2 lg:grid-cols-3">
      <article 
        v-for="post in paginatedPosts" 
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

    <div class="flex items-center justify-between mt-6">
      <button 
        @click="prevSlide" 
        :disabled="currentPage === 1" 
        class="px-4 py-2 text-white bg-gray-500 rounded hover:bg-gray-600 disabled:opacity-50"
      >
        Précédent
      </button>
      <span class="text-lg font-semibold">
        {{ currentPage }} / {{ totalPages }}
      </span>
      <button 
        @click="nextSlide" 
        :disabled="currentPage === totalPages" 
        class="px-4 py-2 text-white bg-gray-500 rounded hover:bg-gray-600 disabled:opacity-50"
      >
        Suivant
      </button>
    </div>

    <div class="flex justify-center mt-4 space-x-2">
      <button 
        v-for="page in totalPages" 
        :key="page" 
        @click="goToPage(page)" 
        :class="['w-8 h-8 flex items-center justify-center rounded-full text-white', page === currentPage ? 'bg-green-500' : 'bg-gray-300 hover:bg-gray-400']"
      >
        {{ page }}
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
      currentPage: 1,
      postsPerPage: 3, // Nombre d'articles par page
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.posts.length / this.postsPerPage);
    },
    paginatedPosts() {
      const start = (this.currentPage - 1) * this.postsPerPage;
      return this.posts.slice(start, start + this.postsPerPage);
    },
  },
  methods: {
    prevSlide() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    nextSlide() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    goToPage(page) {
      this.currentPage = page;
    },
  },
};
</script>

<style scoped>
/* Ajoutez ici des styles spécifiques si nécessaire */
</style>
