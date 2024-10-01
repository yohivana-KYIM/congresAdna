<template>
  <section class="py-12 bg-site-bg">
    <div class="container px-0 mx-auto">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
        <div
          v-for="(slide, index) in slides"
          :key="index"
          class="flex flex-col justify-between h-full p-6 text-center transition-transform duration-300 transform bg-white rounded-lg shadow-lg hover:shadow-xl"
        >
          <div class="relative">
            <img
              :src="`/images/${slide.image}`"
              :alt="'Image ' + (index + 1)"
              class="object-cover w-full h-48 transition-transform duration-500 ease-in-out transform cursor-pointer hover:scale-110"
            />
            <h3
              class="mt-4 text-lg font-semibold text-gray-800 transition-transform duration-300 transform hover:translate-y-[-5px] relative z-10"
            >
              {{ slide.title }}
            </h3>
            <p
              class="text-gray-600 transition-transform duration-300 transform hover:translate-y-[-2px] relative z-10"
            >
              {{ slide.description }}
            </p>
          </div>
          <a
            href="#"
            class="inline-block px-4 py-2 mt-4 text-center text-white transition-colors duration-300 bg-blue-600 rounded-lg hover:bg-blue-700"
          >
            Voir Plus
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'News',
  data() {
    return {
      slides: [
        {
          id: 1,
          title: 'Title 1',
          description: 'Description 1',
          image: 'ev1.jpg',
        },
        {
          id: 2,
          title: 'Title 2',
          description: 'Description 2',
          image: 'ev2.jpg',
        },
        {
          id: 3,
          title: 'Title 3',
          description: 'Description 3',
          image: 'ev3.jpg',
        },
        {
          id: 4,
          title: 'Title 4',
          description: 'Description 4',
          image: 'ev4.jpg',
        },
        {
          id: 5,
          title: 'Title 5',
          description: 'Description 5',
          image: 'ev5.jpg',
        },
        {
          id: 6,
          title: 'Title 6',
          description: 'Description 6',
          image: 'ev6.jpg',
        },
        {
          id: 7,
          title: 'Title 7',
          description: 'Description 7',
          image: 'ev7.jpg',
        },
        {
          id: 8,
          title: 'Title 8',
          description: 'Description 8',
          image: 'ev8.jpg',
        },
        {
          id: 9,
          title: 'Title 9',
          description: 'Description 9',
          image: 'ev9.jpg',
        },

      ],
    };
  },
};
</script>