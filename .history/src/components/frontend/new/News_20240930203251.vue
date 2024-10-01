<template>
  <section class="max-w-6xl py-10 mx-auto">
    <h2 class="mb-6 text-3xl font-bold text-center text-gray-800">Blog du Congrès ADNA</h2>
    <div class="grid grid-cols-1 gap-6 md:grid-cols-2 lg:grid-cols-3">
      <article 
        v-for="post in posts" 
        :key="post.id" 
        class="overflow-hidden bg-white rounded-lg shadow-md transition duration-300 hover:shadow-lg"
      >
        <img 
          :src="post.image" 
          alt="Image de l'article" 
          class="object-cover w-full h-48"
        >
        <div class="p-4">
          <h3 
            class="mb-2 text-xl font-semibold text-gray-900 transition-transform duration-300 transform hover:translate-y-2 hover:bg-green-200 rounded p-1"
          >
            {{ post.title }}
          </h3>
          <p 
            class="mb-4 text-gray-700 transition-transform duration-300 transform hover:-translate-y-1 hover:bg-green-200 rounded p-1"
          >
            {{ post.excerpt }}
          </p>
          <router-link 
            :to="`/blog/${post.id}`" 
            class="inline-block text-blue-500 hover:text-blue-700 transition-colors duration-200"
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
      ],
    };
  },
};
</script>

<style scoped>
/* Ajoutez ici des styles spécifiques si nécessaire */
</style>
