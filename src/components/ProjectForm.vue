<script setup lang="ts">
import { ref } from 'vue'

const projectData = ref({
  // Informations personnelles
  firstName: '',
  lastName: '',
  email: '',
  phone: '',
  address: '',
  city: '',
  postalCode: '',

  // Informations du projet
  projectType: '',
  surface: '',
  budget: '',
  timeframe: '',
  startDate: '',
  description: '',

  // Type de travaux
  works: {
    interiorPainting: false,
    exteriorPainting: false,
    wallpapering: false,
    renovation: false,
    flooring: false,
    other: false
  },

  // Documents
  documents: [] as File[],
  
  // Préférences
  preferredContactMethod: 'email',
  availabilityTime: []
})

const handleFileChange = (event: Event) => {
  const input = event.target as HTMLInputElement
  if (input.files) {
    projectData.value.documents = Array.from(input.files)
  }
}

const handleSubmit = (e: Event) => {
  e.preventDefault()
  console.log('Project form submitted:', projectData.value)
  // Ajoutez ici la logique d'envoi du formulaire
}
</script>

<template>
  <section id="project-form" class="py-20 bg-gray-50">
    <div class="max-w-4xl mx-auto px-4">
      <h2 class="section-title">Déposer un Projet</h2>
      
      <form @submit="handleSubmit" class="bg-white p-8 rounded-lg shadow-lg">
        <!-- Informations personnelles -->
        <div class="mb-8">
          <h3 class="text-xl font-semibold mb-4 text-[#1a4d2e]">Informations Personnelles</h3>
          <div class="grid md:grid-cols-2 gap-4">
            <div>
              <label class="block text-gray-700 mb-2" for="firstName">Prénom *</label>
              <input
                type="text"
                id="firstName"
                v-model="projectData.firstName"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
                required
              >
            </div>
            <div>
              <label class="block text-gray-700 mb-2" for="lastName">Nom *</label>
              <input
                type="text"
                id="lastName"
                v-model="projectData.lastName"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
                required
              >
            </div>
            <div>
              <label class="block text-gray-700 mb-2" for="email">Email *</label>
              <input
                type="email"
                id="email"
                v-model="projectData.email"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
                required
              >
            </div>
            <div>
              <label class="block text-gray-700 mb-2" for="phone">Téléphone *</label>
              <input
                type="tel"
                id="phone"
                v-model="projectData.phone"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
                required
              >
            </div>
            <div class="md:col-span-2">
              <label class="block text-gray-700 mb-2" for="address">Adresse *</label>
              <input
                type="text"
                id="address"
                v-model="projectData.address"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
                required
              >
            </div>
            <div>
              <label class="block text-gray-700 mb-2" for="city">Ville *</label>
              <input
                type="text"
                id="city"
                v-model="projectData.city"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
                required
              >
            </div>
            <div>
              <label class="block text-gray-700 mb-2" for="postalCode">Code Postal *</label>
              <input
                type="text"
                id="postalCode"
                v-model="projectData.postalCode"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
                required
              >
            </div>
          </div>
        </div>

        <!-- Type de travaux -->
        <div class="mb-8">
          <h3 class="text-xl font-semibold mb-4 text-[#1a4d2e]">Type de Travaux</h3>
          <div class="grid md:grid-cols-2 gap-4">
            <div class="flex items-center">
              <input
                type="checkbox"
                id="interiorPainting"
                v-model="projectData.works.interiorPainting"
                class="mr-2"
              >
              <label for="interiorPainting">Peinture intérieure</label>
            </div>
            <div class="flex items-center">
              <input
                type="checkbox"
                id="exteriorPainting"
                v-model="projectData.works.exteriorPainting"
                class="mr-2"
              >
              <label for="exteriorPainting">Peinture extérieure</label>
            </div>
            <div class="flex items-center">
              <input
                type="checkbox"
                id="wallpapering"
                v-model="projectData.works.wallpapering"
                class="mr-2"
              >
              <label for="wallpapering">Pose de papier peint</label>
            </div>
            <div class="flex items-center">
              <input
                type="checkbox"
                id="renovation"
                v-model="projectData.works.renovation"
                class="mr-2"
              >
              <label for="renovation">Rénovation</label>
            </div>
            <div class="flex items-center">
              <input
                type="checkbox"
                id="flooring"
                v-model="projectData.works.flooring"
                class="mr-2"
              >
              <label for="flooring">Revêtement de sol</label>
            </div>
            <div class="flex items-center">
              <input
                type="checkbox"
                id="other"
                v-model="projectData.works.other"
                class="mr-2"
              >
              <label for="other">Autre</label>
            </div>
          </div>
        </div>

        <!-- Informations du projet -->
        <div class="mb-8">
          <h3 class="text-xl font-semibold mb-4 text-[#1a4d2e]">Informations du Projet</h3>
          <div class="grid md:grid-cols-2 gap-4">
            <div>
              <label class="block text-gray-700 mb-2" for="surface">Surface approximative (m²)</label>
              <input
                type="number"
                id="surface"
                v-model="projectData.surface"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
              >
            </div>
            <div>
              <label class="block text-gray-700 mb-2" for="budget">Budget estimé (€)</label>
              <input
                type="number"
                id="budget"
                v-model="projectData.budget"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
              >
            </div>
            <div>
              <label class="block text-gray-700 mb-2" for="startDate">Date souhaitée de début</label>
              <input
                type="date"
                id="startDate"
                v-model="projectData.startDate"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
              >
            </div>
            <div>
              <label class="block text-gray-700 mb-2" for="timeframe">Délai souhaité</label>
              <select
                id="timeframe"
                v-model="projectData.timeframe"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
              >
                <option value="">Sélectionnez un délai</option>
                <option value="urgent">Urgent (< 1 mois)</option>
                <option value="1-3months">1 à 3 mois</option>
                <option value="3-6months">3 à 6 mois</option>
                <option value="6+months">Plus de 6 mois</option>
              </select>
            </div>
          </div>
          <div class="mt-4">
            <label class="block text-gray-700 mb-2" for="description">Description détaillée du projet *</label>
            <textarea
              id="description"
              v-model="projectData.description"
              rows="4"
              class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
              required
            ></textarea>
          </div>
        </div>

        <!-- Documents -->
        <div class="mb-8">
          <h3 class="text-xl font-semibold mb-4 text-[#1a4d2e]">Documents</h3>
          <div class="border-2 border-dashed border-gray-300 rounded-lg p-4">
            <input
              type="file"
              id="documents"
              @change="handleFileChange"
              multiple
              class="hidden"
            >
            <label
              for="documents"
              class="block text-center cursor-pointer text-gray-600 hover:text-[#1a4d2e]"
            >
              <svg class="w-8 h-8 mx-auto mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
              </svg>
              Cliquez pour ajouter des photos ou documents
            </label>
          </div>
          <p class="text-sm text-gray-500 mt-2">
            Formats acceptés : JPG, PNG, PDF (Max 5Mo par fichier)
          </p>
        </div>

        <!-- Préférences de contact -->
        <div class="mb-8">
          <h3 class="text-xl font-semibold mb-4 text-[#1a4d2e]">Préférences de Contact</h3>
          <div>
            <label class="block text-gray-700 mb-2">Méthode de contact préférée</label>
            <div class="flex space-x-4">
              <label class="flex items-center">
                <input
                  type="radio"
                  v-model="projectData.preferredContactMethod"
                  value="email"
                  class="mr-2"
                >
                Email
              </label>
              <label class="flex items-center">
                <input
                  type="radio"
                  v-model="projectData.preferredContactMethod"
                  value="phone"
                  class="mr-2"
                >
                Téléphone
              </label>
            </div>
          </div>
        </div>

        <button type="submit" class="btn-primary w-full">Envoyer mon projet</button>
      </form>
    </div>
  </section>
</template>