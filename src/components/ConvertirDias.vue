<template>
  <div class="max-w-md mx-auto p-8 bg-white shadow-lg rounded-lg">
    <h2 class="text-2xl font-bold text-center mb-4">Conversión de Días a Años, Semanas y Días</h2>

    <div class="mb-4">
      <label for="dias" class="block text-sm font-medium text-gray-700">Número de días:</label>
      <input v-model.number="days" type="number" id="days"
        class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
        placeholder="Ingresa el número de días" />
    </div>

    <button @click="convertir"
      class="w-full bg-indigo-600 text-white py-2 px-4 rounded-md hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-opacity-50">
      Convertir
    </button>

    <div v-if="error" class="mt-4 text-red-600 text-sm">
      {{ error }}
    </div>

    <div v-if="results" class="mt-4 space-y-2">
      <p><strong>Años:</strong> {{ results.years }}</p>
      <p><strong>Semanas:</strong> {{ results.weeks }}</p>
      <p><strong>Días:</strong> {{ results.restDays }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

// Definimos una interfaz 'Results' que describe la estructura del objeto de resultados
interface Results {
  years: number;
  weeks: number;
  restDays: number;
}
// Declaramos 'days' como una referencia reactiva que inicialmente es 'null'.
// Esta referencia almacenará la cantidad de días ingresada por el usuario.
const days = ref<null>(null);
const results = ref<Results | null>(null);
const error = ref<string>('');

const convertir = () => {
  if (days.value !== null && days.value >= 0) {
    error.value = ''; // Limpiar mensaje de error
    const years = Math.floor(days.value / 365); // Cantidad de años dividiendo por los 365 dias
    const weeks = Math.floor((days.value % 365) / 7); // El residuo del calculo anterior dividido por los dias de la semana
    const restDays = (days.value % 365) % 7;

    results.value = { years, weeks, restDays };
  } else {
    // Caso de error
    results.value = null;
    error.value = "Por favor, ingresa un número válido."
  }
};
</script>
