<template>
  <header class="py-4 shadow-md bg-site-bg">
    <div class="container px-4 mx-auto">
      <div class="flex flex-col items-center justify-between p-4 transition-all duration-300 ease-in-out bg-white rounded-lg shadow-lg md:flex-row hover:shadow-xl">
        <!-- Logo et titre -->
        <div class="flex items-center mb-4 transition-transform duration-300 ease-in-out md:mb-0 hover:scale-105">
          <img src="/images/logo/logo-adna.png" alt="Logo ADNA" class="w-auto h-12 mr-3">
          <h1 class="text-lg font-bold text-yellow-700 transition-colors duration-300 ease-in-out hover:text-yellow-600">
            CONGRES NDOGBATJECK
          </h1>
        </div>
        
        <!-- Informations du congrès -->
        <div class="mb-4 text-center md:text-right md:mb-0">
          <p class="text-sm font-semibold text-gray-700">
            📅 23 au 26 Janvier 2025
          </p>
          <p class="text-xs text-gray-600">
            EKOANGOMBE SUD - MANGOG
          </p>
        </div>
        
        <!-- Compte à rebours et contrôles -->
        <div class="flex flex-col items-center">
          <div class="mb-2 text-2xl font-bold text-red-600" :class="{ 'animate-pulse': isRunning }">
            {{ displayText }}
          </div>
          <div class="flex space-x-2">
            <button 
              @click="toggleCountdown" 
              class="px-4 py-2 text-sm font-semibold transition-colors duration-300 ease-in-out rounded-full"
              :class="isRunning ? 'bg-red-500 hover:bg-red-600 text-white' : 'bg-green-500 hover:bg-green-600 text-white'"
            >
              {{ isRunning ? 'Arrêter' : 'Démarrer' }}
            </button>
            <button 
              @click="resetCountdown" 
              class="px-4 py-2 text-sm font-semibold text-white transition-colors duration-300 ease-in-out bg-blue-500 rounded-full hover:bg-blue-600"
</style>