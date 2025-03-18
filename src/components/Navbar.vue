<script setup lang="ts">
import { ref } from 'vue'

const isMenuOpen = ref(false)

const scrollToSection = (sectionId: string) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
    isMenuOpen.value = false
  }
}
</script>

<template>
  <nav class="bg-white shadow-lg fixed w-full z-50">
    <div class="max-w-7xl mx-auto px-4">
      <div class="flex justify-between h-16">
        <div class="flex items-center">
          <h1 class="text-2xl font-bold text-blue-600">Peinture & Rénovation</h1>
        </div>
        
        <!-- Desktop Menu -->
        <div class="hidden md:flex items-center space-x-8">
          <button @click="scrollToSection('accueil')" class="text-gray-700 hover:text-blue-600">Accueil</button>
          <button @click="scrollToSection('services')" class="text-gray-700 hover:text-blue-600">Services</button>
          <button @click="scrollToSection('about')" class="text-gray-700 hover:text-blue-600">À propos</button>
          <button @click="scrollToSection('contact')" class="text-gray-700 hover:text-blue-600">Contact</button>
          <button @click="scrollToSection('project-form')" class="btn-primary">Déposer un projet</button>

        </div>

        <!-- Mobile Menu Button -->
        <div class="md:hidden flex items-center">
          <button @click="isMenuOpen = !isMenuOpen" class="text-gray-700">
            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path v-if="!isMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
              <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- Mobile Menu -->
    <div v-if="isMenuOpen" class="md:hidden">
      <div class="px-2 pt-2 pb-3 space-y-1 bg-white">
        <button @click="scrollToSection('accueil')" class="block w-full text-left px-3 py-2 text-gray-700 hover:text-blue-600">Accueil</button>
        <button @click="scrollToSection('services')" class="block w-full text-left px-3 py-2 text-gray-700 hover:text-blue-600">Services</button>
        <button @click="scrollToSection('about')" class="block w-full text-left px-3 py-2 text-gray-700 hover:text-blue-600">À propos</button>
        <button @click="scrollToSection('contact')" class="block w-full text-left px-3 py-2 text-gray-700 hover:text-blue-600">Contact</button>
        <button @click="scrollToSection('project-form')" class="block w-full px-3 py-2 btn-primary text-center">Déposer un projet</button>
        <button @click="scrollToSection('payment')" class="block w-full px-3 py-2 btn-secondary text-center">Paiement</button>
      </div>
    </div>
  </nav>
</template>