<template>
  <!-- Division  -->
  <div class="divider"></div>
</template>

<script>
export default {
  name: 'Separator'
}
</script>

<style scoped>
.divider {
  background-color: #fff;
  height: 8px; /* Doubler la hauteur pour rendre la ligne plus épaisse */
  width: 80%; /* Ajustez ici pour diminuer la longueur */
  margin: 0 auto; /* Centrer horizontalement */
}

.transition-transform {
  transition: transform 0.5s ease-out; /* Transition fluide pour la rotation */
}
</style>
