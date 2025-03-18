<script setup lang="ts">
import { ref } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'

const formData = ref({
  name: '',
  email: '',
  phone: '',
  subject: '',
  message: '',
  newsletter: false
})

const formRef = ref(null)
const isVisible = ref(false)

useIntersectionObserver(formRef, ([{ isIntersecting }]) => {
  if (isIntersecting) isVisible.value = true
})

const handleSubmit = async (e: Event) => {
  e.preventDefault()
  // Animation de confirmation
  const button = (e.target as HTMLFormElement).querySelector('button')
  if (button) {
    button.classList.add('success')
    setTimeout(() => button.classList.remove('success'), 2000)
  }
  console.log('Form submitted:', formData.value)
}
</script>

<template>
  <section id="contact" class="py-20 bg-gradient-to-b from-gray-50 to-white">
    <div class="max-w-4xl mx-auto px-4">
      <div class="text-center mb-12">
        <h2 class="text-3xl font-bold text-blue-600 mb-4">Contactez-nous</h2>
        <p class="text-gray-600 max-w-2xl mx-auto">
          Une question ? Un projet ? N'hésitez pas à nous contacter. Notre équipe vous répondra dans les plus brefs délais.
        </p>
      </div>

      <div
        ref="formRef"
        :class="['bg-white rounded-2xl shadow-xl p-8 transition-all duration-700 transform', 
                isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0']"
      >
        <form @submit="handleSubmit" class="space-y-6">
          <div class="grid md:grid-cols-2 gap-6">
            <!-- Nom -->
            <div class="relative">
              <input
                type="text"
                id="name"
                v-model="formData.name"
                required
                class="peer w-full px-4 py-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:outline-none transition-colors bg-gray-50 placeholder-transparent"
                placeholder="Votre nom"
              >
              <label
                for="name"
                class="absolute left-4 -top-2.5 bg-white px-2 text-sm text-gray-600 transition-all peer-placeholder-shown:top-3 peer-placeholder-shown:text-base peer-placeholder-shown:bg-transparent peer-focus:-top-2.5 peer-focus:text-sm peer-focus:bg-white"
              >
                Votre nom
              </label>
            </div>

            <!-- Email -->
            <div class="relative">
              <input
                type="email"
                id="email"
                v-model="formData.email"
                required
                class="peer w-full px-4 py-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:outline-none transition-colors bg-gray-50 placeholder-transparent"
                placeholder="Votre email"
              >
              <label
                for="email"
                class="absolute left-4 -top-2.5 bg-white px-2 text-sm text-gray-600 transition-all peer-placeholder-shown:top-3 peer-placeholder-shown:text-base peer-placeholder-shown:bg-transparent peer-focus:-top-2.5 peer-focus:text-sm peer-focus:bg-white"
              >
                Votre email
              </label>
            </div>

            <!-- Téléphone -->
            <div class="relative">
              <input
                type="tel"
                id="phone"
                v-model="formData.phone"
                required
                class="peer w-full px-4 py-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:outline-none transition-colors bg-gray-50 placeholder-transparent"
                placeholder="Votre téléphone"
              >
              <label
                for="phone"
                class="absolute left-4 -top-2.5 bg-white px-2 text-sm text-gray-600 transition-all peer-placeholder-shown:top-3 peer-placeholder-shown:text-base peer-placeholder-shown:bg-transparent peer-focus:-top-2.5 peer-focus:text-sm peer-focus:bg-white"
              >
                Votre téléphone
              </label>
            </div>

            <!-- Sujet -->
            <div class="relative">
              <input
                type="text"
                id="subject"
                v-model="formData.subject"
                required
                class="peer w-full px-4 py-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:outline-none transition-colors bg-gray-50 placeholder-transparent"
                placeholder="Sujet"
              >
              <label
                for="subject"
                class="absolute left-4 -top-2.5 bg-white px-2 text-sm text-gray-600 transition-all peer-placeholder-shown:top-3 peer-placeholder-shown:text-base peer-placeholder-shown:bg-transparent peer-focus:-top-2.5 peer-focus:text-sm peer-focus:bg-white"
              >
                Sujet
              </label>
            </div>
          </div>

          <!-- Message -->
          <div class="relative">
            <textarea
              id="message"
              v-model="formData.message"
              rows="4"
              required
              class="peer w-full px-4 py-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:outline-none transition-colors bg-gray-50 placeholder-transparent"
              placeholder="Votre message"
            ></textarea>
            <label
              for="message"
              class="absolute left-4 -top-2.5 bg-white px-2 text-sm text-gray-600 transition-all peer-placeholder-shown:top-3 peer-placeholder-shown:text-base peer-placeholder-shown:bg-transparent peer-focus:-top-2.5 peer-focus:text-sm peer-focus:bg-white"
            >
              Votre message
            </label>
          </div>

          <!-- Newsletter -->
          <div class="flex items-center space-x-3">
            <input
              type="checkbox"
              id="newsletter"
              v-model="formData.newsletter"
              class="w-5 h-5 text-blue-600 border-2 border-gray-300 rounded focus:ring-blue-500"
            >
            <label for="newsletter" class="text-gray-700">
              Je souhaite recevoir la newsletter
            </label>
          </div>

          <!-- Submit Button -->
          <button
            type="submit"
            class="w-full bg-blue-600 text-white py-3 px-6 rounded-lg hover:bg-blue-700 transform hover:scale-[1.02] transition-all duration-300 relative overflow-hidden group"
          >
            <span class="relative z-10">Envoyer le message</span>
            <span class="absolute inset-0 bg-green-500 transform scale-x-0 group-[.success]:scale-x-100 transition-transform duration-500 origin-left"></span>
            <span class="absolute inset-0 flex items-center justify-center text-white opacity-0 group-[.success]:opacity-100 transition-opacity duration-500">
              Message envoyé !
            </span>
          </button>
        </form>

        <!-- Contact Info -->
        <div class="mt-12 grid md:grid-cols-3 gap-8">
          <div class="text-center">
            <div class="w-12 h-12 mx-auto mb-4 bg-blue-100 rounded-full flex items-center justify-center">
              <svg class="w-6 h-6 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
              </svg>
            </div>
            <h3 class="font-semibold mb-2">Téléphone</h3>
            <p class="text-gray-600">01 23 45 67 89</p>
          </div>

          <div class="text-center">
            <div class="w-12 h-12 mx-auto mb-4 bg-blue-100 rounded-full flex items-center justify-center">
              <svg class="w-6 h-6 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
              </svg>
            </div>
            <h3 class="font-semibold mb-2">Email</h3>
            <p class="text-gray-600">contact@lemaire-renovation.fr</p>
          </div>

          <div class="text-center">
            <div class="w-12 h-12 mx-auto mb-4 bg-blue-100 rounded-full flex items-center justify-center">
              <svg class="w-6 h-6 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
            </div>
            <h3 class="font-semibold mb-2">Adresse</h3>
            <p class="text-gray-600">123 Rue de la Rénovation, 75015 Paris</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.peer:focus ~ label,
.peer:not(:placeholder-shown) ~ label {
  @apply -top-2.5 text-sm bg-white;
}

@keyframes checkmark {
  0% { transform: scale(0); }
  100% { transform: scale(1); }
}
</style>