// views/Home.vue
<template>
  <div class="home">
    <Separator />
    <br />
    <HeroBanner />
    <br />
    <Separator />
    <div class="bg-[#458018] p-4 rounded-full text-white text-center mt-8 w-1/2 mx-auto">À propos du Congrès</div>

    <AboutCongress />
    <Separator />
    <div class="bg-[#458018] p-4 rounded-full text-white text-center mt-8 w-1/2 mx-auto">ACTUALITES</div>


    <News />
    <Separator />
    <div class="bg-[#458018] p-4 rounded-full text-white text-center mt-8 w-1/2 mx-auto">Nos Partenaires</div>

    <br />
    <Partners /><br />
   <Separator /><br />
    <TempsFort />
    
  </div>
</template>

<script>
import HeroBanner from '@/components/frontend/heroBanner/HeroBanner.vue'
import AboutCongress from '@/components/frontend/aboutCongress/AboutCongress.vue'
import News from '@/components/frontend/new/News.vue'
import Partners from '@/components/frontend//partner/Partners.vue'
import TempsFort from '@/components/frontend/tempsFort/TempsFort.vue'
import Separator from '@/components/frontend/separator/Separator.vue'

export default {
  name: 'Home',
  components: {
    HeroBanner,
    AboutCongress,
    News,
    Partners,
    TempsFort,
    Separator
  }
}
</script>