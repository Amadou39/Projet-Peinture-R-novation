<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'

const slides = [
  {
    image: 'https://www.toutelapeinture.fr/wp-content/uploads/2022/07/NUDE-1-scaled.jpg',
    title: 'Peinture Intérieure',
    description: 'Des finitions impeccables pour vos intérieurs'
  },
  {
    image: 'https://www.travauxapart.fr/sites/default/files/renovation-complete.jpg',
    title: 'Rénovation Complète',
    description: 'Transformez votre espace de vie'
  },
  {
    image: 'https://beltran-peinture.com/uploads/media/images/cms/medias/thumb_/cms/medias/668ff2aeb7878_images_large.jpeg',
    title: 'Peinture Extérieure',
    description: 'Embellissez votre façade'
  }
]

const currentSlide = ref(0)
let intervalId: number | null = null

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % slides.length
}

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + slides.length) % slides.length
}

onMounted(() => {
  intervalId = setInterval(nextSlide, 5000)
})

onBeforeUnmount(() => {
  if (intervalId) clearInterval(intervalId)
})
</script>

<template>
  <section id="accueil" class="relative h-screen">
    <div class="absolute inset-0">
      <transition-group name="fade">
        <div
          v-for="(slide, index) in slides"
          :key="index"
          v-show="currentSlide === index"
          class="absolute inset-0"
        >
          <div
            class="absolute inset-0 bg-cover bg-center transition-opacity duration-500"
            :style="{ backgroundImage: `url(${slide.image})` }"
          >
            <div class="absolute inset-0 bg-black bg-opacity-50"></div>
          </div>
        </div>
      </transition-group>
    </div>

    <!-- Contrôles du carrousel -->
    <button
      @click="prevSlide"
      class="absolute left-4 top-1/2 transform -translate-y-1/2 bg-white bg-opacity-50 p-2 rounded-full hover:bg-opacity-75 transition-all z-10"
    >
      <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
      </svg>
    </button>
    <button
      @click="nextSlide"
      class="absolute right-4 top-1/2 transform -translate-y-1/2 bg-white bg-opacity-50 p-2 rounded-full hover:bg-opacity-75 transition-all z-10"
    >
      <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
      </svg>
    </button>

    <!-- Indicateurs -->
    <div class="absolute bottom-4 left-1/2 transform -translate-x-1/2 flex space-x-2 z-10">
      <button
        v-for="(_, index) in slides"
        :key="index"
        @click="currentSlide = index"
        class="w-3 h-3 rounded-full transition-all"
        :class="currentSlide === index ? 'bg-white' : 'bg-white bg-opacity-50'"
      ></button>
    </div>

    <div class="relative h-full flex items-center justify-center text-center text-white px-4">
      <div>
        <h1 class="text-4xl md:text-6xl font-bold mb-4">{{ slides[currentSlide].title }}</h1>
        <p class="text-xl md:text-2xl mb-8">{{ slides[currentSlide].description }}</p>
        <a href="#contact" class="btn-primary text-lg">Demander un devis</a>
      </div>
    </div>
  </section>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>