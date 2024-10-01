
        // {
        //   id: 9,
        //   title: 'Title 9',
        //   description: 'Description 9',
        //   image: 'ev9.jpg',
        // },




        <template>
          <section class="max-w-6xl py-10 mx-auto">
            <h2 class="mb-6 text-3xl font-bold text-center">Blog du Congrès ADNA</h2>
            <div class="grid grid-cols-1 gap-6 md:grid-cols-2 lg:grid-cols-3">
              <article v-for="post in posts" :key="post.id" class="overflow-hidden bg-white rounded-lg shadow-md">
                <img :src="post.image" alt="Image de l'article" class="object-cover w-full h-48">
                <div class="p-4">
                  <h3 class="mb-2 text-xl font-semibold">{{ post.title }}</h3>
                  <p class="mb-4 text-gray-700">{{ post.excerpt }}</p>
                  <router-link :to="`/blog/${post.id}`" class="text-blue-500 hover:underline">Lire la suite</router-link>
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
                  image: 'https://via.placeholder.com/400x200',
                },
                {
                  id: 2,
                  title: 'Conférenciers et Thèmes',
                  excerpt: 'Rencontrez nos conférenciers invités et explorez les thèmes qui seront abordés.',
                  image: 'https://via.placeholder.com/400x200',
                },
                {
                  id: 3,
                  title: 'Inscription et Tarification',
                  excerpt: 'Tous les détails concernant l\'inscription au congrès et les options de tarification.',
                  image: 'https://via.placeholder.com/400x200',
                },
              ],
            };
          },
        };
        </script>
        
        <style scoped>
        /* Ajoutez ici des styles spécifiques si nécessaire */
        </style>
        