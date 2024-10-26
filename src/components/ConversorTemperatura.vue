<template>
  <div class="max-w-md mx-auto p-8 bg-white shadow-lg rounded-lg">
    <h2 class="text-2xl font-bold text-center mb-4">Conversión de Temperatura</h2>
    <!-- Input para ingresar los valores -->
    <div class="mb-4">
      <label for="celsius" class="block text-sm font-medium text-gray-700">Grados Celsius:</label>
      <input
        v-model.number="celsius"
        type="number"
        id="celsius"
        class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
        placeholder="Ingresa la temperatura en grados Celsius"
      />
    </div>
    <!-- Boton para convertir -->
    <button
      @click="convertir"
      class="w-full bg-indigo-600 text-white py-2 px-4 rounded-md hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-opacity-50"
    >
      Convertir
    </button>
    <!-- Manejo de errores -->
    <div v-if="error" class="mt-4 text-red-600 text-sm">
      {{ error }}
    </div>

    <div v-if="results" class="mt-4 space-y-2">
      <p>Kelvin: <span class="font-semibold">{{ results.kelvin }}</span></p>
      <p>Fahrenheit: <span class="font-semibold">{{ results.fahrenheit }}</span></p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
  interface Results {
    kelvin: string;
    fahrenheit: string;
  }
  const celsius = ref<number | null>(null);
  const results = ref<Results | null>(null);
  const error = ref<string>('');

  const convertir = ():void => {
      if (celsius.value !== null || celsius.value !== "") {
        error.value = ''; // Limpiar cualquier error previo
        results.value = {
          kelvin: (celsius.value! + 273.15).toFixed(2),
          fahrenheit: ((celsius.value! * 9) / 5 + 32).toFixed(2),
        };
      } else {
        results.value = null;
        error.value = 'Por favor, ingresa un valor en grados Celsius.'; 
      }
    };

</script>

<style scoped>
.error {
  color: red;
}
</style>
