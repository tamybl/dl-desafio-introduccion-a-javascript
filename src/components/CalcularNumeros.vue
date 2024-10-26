<template>
    <div class="max-w-md mx-auto p-8 bg-white shadow-lg rounded-lg">
      <h2 class="text-2xl font-bold text-center mb-4">Ingresar 5 Números</h2>
  
      <!-- Input para ingresar los 5 numeros -->
      <div v-for="(number, index) in numbers" :key="index" class="mb-4">
        <label :for="'number' + index" class="block text-sm font-medium text-gray-700">Número {{ index + 1 }}:</label>
        <input
          v-model.number="numbers[index]"
          type="number"
          :id="'number-' + index"
          class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
          :placeholder="'Ingresa el número ' + (index + 1)"
        />
      </div>
  
      <!-- Boton para calculo -->
      <button
        @click="calculateResults"
        class="w-full bg-indigo-600 text-white py-2 px-4 rounded-md hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-opacity-50"
      >
        Calcular
      </button>
  
      <!-- Se despliega error si aplica -->
      <div v-if="error" class="mt-4 text-red-600 text-sm">
        {{ error }}
      </div>
  
      <!-- Seccion de resultados -->
      <div v-if="results" class="mt-4 space-y-2">
        <p><strong>Suma:</strong> {{ results.sum }}</p>
        <p><strong>Promedio:</strong> {{ results.average }}</p>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  
    interface Results {
        sum: number;
        average: number;
    }
    const numbers = ref([null, null, null, null, null]); // Arreglo de 5 numeros
    const results = ref<Results | null>(null);
    const error = ref<string>('');
  
    const calculateResults = ():void => {
        // Verificar si todos los numeros son enteros y el campo no está vacío
        if (numbers.value.every(num => num !== null && num !== '')) {
          const sum = numbers.value.reduce((acc, num) => acc + num, 0); // Sumatorio
          const average = sum / numbers.value.length; // Promedio
          results.value = { sum, average };
          error.value = ''; // Limpiar mensaje de error
        } else {
          results.value = null;
          error.value = 'Por favor, ingresa los 5 números.';
        }
      };
  
  </script>