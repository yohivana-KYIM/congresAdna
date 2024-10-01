<template>
  <section class="container px-4 py-8 mx-auto">
    <h2 class="mb-8 text-3xl font-bold text-center text-gray-800">
      Blog du Congrès ADNA
    </h2>
    
    <div class="grid grid-cols-1 gap-6 md:grid-cols-2 lg:grid-cols-3">
      <article 
        v-for="post in posts" 
        :key="post.id" 
        class="transition-all duration-300 hover:shadow-sm"
      >
        <div class="overflow-hidden rounded-lg aspect-w-16 aspect-h-9">
          <img 
            :src="post.image" 
            :alt="post.title" 
            class="object-cover w-full h-full"
            v-lazy-load
          >
        </div>
        
        <div class="p-4 mt-4">
          <h3 
            class="mb-2 text-xl font-semibold text-gray-900"
            v-text="post.title"
          ></h3>
          
          <p 
            class="mb-4 text-gray-700"
            v-text="post.excerpt"
          ></p>
          
          <router-link 
            :to="`/blog/${post.id}`" 
            class="inline-block text-blue-500 transition-colors duration-200 hover:text-blue-700"
            aria-label="Lire la suite"
          >
            Lire la suite
          </router-link>
        </div>
      </article>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue';

const posts = [
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
];

const filteredPosts = computed(() => posts.filter(post => post.title.toLowerCase().includes('conférenciers')));
</script>

<style scoped>
@layer components {
  .blog-post {
    @apply rounded-lg bg-white shadow-md overflow-hidden transition-all duration-300 hover:shadow-lg;
  }

  .blog-image {
    @apply w-full h-auto;
  }

  .blog-content {
    @apply px-4 py-4;
  }
}
</style>
