<script setup lang="ts">
import { ref } from 'vue';

const paymentData = ref({
  cardNumber: '',
  cardHolder: '',
  expiryDate: '',
  cvv: '',
  amount: '',
  email: '',
  invoiceNumber: '',
});

const formatCardNumber = (value: string) => {
  const v = value.replace(/\s+/g, '').replace(/[^0-9]/gi, '');
  const matches = v.match(/\d{4,16}/g);
  const match = (matches && matches[0]) || '';
  const parts = [];

  for (let i = 0, len = match.length; i < len; i += 4) {
    parts.push(match.substring(i, i + 4));
  }

  if (parts.length) {
    return parts.join(' ');
  } else {
    return value;
  }
};

const handleSubmit = (e: Event) => {
  e.preventDefault();
  // Ici, vous ajouteriez la logique de traitement du paiement
  console.log('Payment submitted:', paymentData.value);
};
</script>

<template>
  <section id="payment" class="py-20 bg-gray-50">
    <div class="max-w-2xl mx-auto px-4">
      <h2 class="section-title">Paiement Sécurisé</h2>

      <form @submit="handleSubmit" class="bg-white p-8 rounded-lg shadow-lg">
        <!-- Montant et Référence -->
        <div class="mb-8">
          <div class="grid md:grid-cols-2 gap-4">
            <div>
              <label class="block text-gray-700 mb-2" for="amount"
                >Montant à payer (€) *</label
              >
              <input
                type="number"
                id="amount"
                v-model="paymentData.amount"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
                required
                min="1"
                step="0.01"
              />
            </div>
            <div>
              <label class="block text-gray-700 mb-2" for="invoiceNumber"
                >Numéro de facture *</label
              >
              <input
                type="text"
                id="invoiceNumber"
                v-model="paymentData.invoiceNumber"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
                required
              />
            </div>
          </div>
        </div>

        <!-- Informations de carte -->
        <div class="mb-8">
          <h3 class="text-xl font-semibold mb-4 text-[#1a4d2e]">
            Informations de Carte
          </h3>
          <div class="space-y-4">
            <div>
              <label class="block text-gray-700 mb-2" for="cardNumber"
                >Numéro de carte *</label
              >
              <input
                type="text"
                id="cardNumber"
                v-model="paymentData.cardNumber"
                @input="
                  paymentData.cardNumber = formatCardNumber($event.target.value)
                "
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
                maxlength="19"
                required
                placeholder="1234 5678 9012 3456"
              />
            </div>
            <div>
              <label class="block text-gray-700 mb-2" for="cardHolder"
                >Nom sur la carte *</label
              >
              <input
                type="text"
                id="cardHolder"
                v-model="paymentData.cardHolder"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
                required
              />
            </div>
            <div class="grid grid-cols-2 gap-4">
              <div>
                <label class="block text-gray-700 mb-2" for="expiryDate"
                  >Date d'expiration *</label
                >
                <input
                  type="text"
                  id="expiryDate"
                  v-model="paymentData.expiryDate"
                  class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
                  required
                  placeholder="MM/AA"
                  maxlength="5"
                />
              </div>
              <div>
                <label class="block text-gray-700 mb-2" for="cvv">CVV *</label>
                <input
                  type="text"
                  id="cvv"
                  v-model="paymentData.cvv"
                  class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
                  required
                  maxlength="4"
                  placeholder="123"
                />
              </div>
            </div>
          </div>
        </div>

        <!-- Email pour reçu -->
        <div class="mb-8">
          <label class="block text-gray-700 mb-2" for="email"
            >Email pour le reçu *</label
          >
          <input
            type="email"
            id="email"
            v-model="paymentData.email"
            class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-[#1a4d2e]"
            required
          />
        </div>

        <!-- Sécurité -->
        <div class="mb-8">
          <div class="bg-gray-50 p-4 rounded-lg">
            <div class="flex items-center mb-2">
              <svg
                class="w-5 h-5 text-[#1a4d2e] mr-2"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"
                />
              </svg>
              <span class="font-semibold">Paiement Sécurisé</span>
            </div>
            <p class="text-sm text-gray-600">
              Vos informations de paiement sont sécurisées. Nous utilisons le
              cryptage SSL pour protéger vos données.
            </p>
          </div>
        </div>

        <button type="submit" class="btn-primary w-full">
          Payer {{ paymentData.amount ? `${paymentData.amount}€` : '' }}
        </button>
      </form>
    </div>
  </section>
</template>
