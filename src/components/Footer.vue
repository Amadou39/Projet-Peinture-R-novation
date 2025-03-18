<template>
  <footer class="bg-gray-900 text-white py-12">
    <div class="max-w-7xl mx-auto px-4">
      <div class="grid md:grid-cols-3 gap-8">
        <div>
          <h3 class="text-xl font-semibold mb-4">Lemaire Peinture</h3>
          <p class="text-gray-400">
            Expert en peinture et rénovation depuis plus de 20 ans. Qualité et satisfaction garanties.
          </p>
        </div>
        <div>
          <h3 class="text-xl font-semibold mb-4">Navigation</h3>
          <ul class="space-y-2">
            <li><a href="#accueil" class="text-gray-400 hover:text-white">Accueil</a></li>
            <li><a href="#services" class="text-gray-400 hover:text-white">Services</a></li>
            <li><a href="#about" class="text-gray-400 hover:text-white">À propos</a></li>
            <li><a href="#contact" class="text-gray-400 hover:text-white">Contact</a></li>
          </ul>
        </div>
        <div>
          <h3 class="text-xl font-semibold mb-4">Contact</h3>
          <ul class="space-y-2 text-gray-400">
            <li>123 Rue de la Rénovation</li>
            <li>75015 Paris</li>
            <li>01 23 45 67 89</li>
            <li>contact@lemaire-renovation.fr</li>
          </ul>
        </div>
      </div>
      <div class="border-t border-gray-800 mt-8 pt-8 text-center text-gray-400">
        <p>&copy; {{ new Date().getFullYear() }} Lemaire Peinture Rénovation. Tous droits réservés.</p>
      </div>
    </div>
  </footer>
</template>