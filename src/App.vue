<script setup lang="ts">
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import Services from './components/Services.vue'
import About from './components/About.vue'
import Contact from './components/Contact.vue'
import ProjectForm from './components/ProjectForm.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div class="min-h-screen">
    <Navbar />
    <main>
      <Hero />
      <Services />
      <About />
      <ProjectForm />
      <Contact />
    </main>
    <Footer />
  </div>
</template>