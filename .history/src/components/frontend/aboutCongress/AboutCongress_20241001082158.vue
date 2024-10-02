<template>
  <div class="flex flex-col p-4 md:p-8 bg-site-bg md:flex-row md:space-x-6">
    <!-- Left Section: Image -->
    <div class="order-1 w-full p-4 md:w-1/3 md:p-6">
      <img src="../assets/images/temps-fort.jpg" alt="Congrès Ndogbatjeck" class="w-full h-auto rounded-lg shadow-lg">
    </div>

    <!-- Right Section: Text -->
    <div class="order-2 w-full p-4 md:w-2/3 md:p-6">
      <p class="mb-4 text-sm text-white md:text-base">
        Le Congrès Ndogbatjeck est un évènement annuel visant à rassembler la communauté Ndogbatjeck pour célébrer son riche patrimoine culturel, renforcer les liens sociaux et discuter des enjeux communautaires. Depuis 1995, cet évènement permet de préserver les traditions tout en abordant des questions actuelles comme le développement local et la solidarité.
      </p>
      <p class="mt-4 text-sm font-bold text-black md:text-base">Dates et lieux:</p> 
      <p class="mb-4 text-sm text-white md:text-base">
        Le prochain congrès se déroulera du 23 au 26 janvier 2026 dans le village Bassa, situé dans la région du Littoral Cameroun. Ce lieu historique accueillera des festivités et des échanges enrichissants autour de la culture et des défis contemporains de la communauté.
      </p>
      <p class="mt-4 text-sm font-bold md:text-base" style="color: #FFCA1D;">Programme:</p> 
      <ul class="ml-4 text-white list-disc md:ml-6">
        <li>23 janvier : Cérémonie d'ouverture et présentation culturelle.</li>
        <li>24 janvier : Ateliers d'entrepreneuriat et discussions sur l'éducation.</li>
        <li>25 janvier : Table ronde sur le développement durable et le rôle des jeunes.</li>
        <li>26 janvier : Cérémonie de clôture et remise de distinctions.</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AboutCongress'
}
</script>
