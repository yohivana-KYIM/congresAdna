
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

