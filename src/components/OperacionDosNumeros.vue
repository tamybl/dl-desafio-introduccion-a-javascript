<template>
  <div class="max-w-md mx-auto p-8 bg-white shadow-lg rounded-lg">
    <h2 class="text-2xl font-bold text-center mb-4">Operaciones con dos números</h2>

    <div class="mb-4">
      <label for="num1" class="block text-sm font-medium text-gray-700">Número 1:</label>
      <input v-model.number="num1" type="number" id="num1"
        class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
        placeholder="Ingresa un número mayor a cero" />
    </div>

    <div class="mb-4">
      <label for="num2" class="block text-sm font-medium text-gray-700">Número 2:</label>
      <input v-model.number="num2" type="number" id="num2"
        class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
        placeholder="Ingresa un número mayor a cero" />
    </div>

    <button @click="calcularOperaciones"
      class="w-full bg-indigo-600 text-white py-2 px-4 rounded-md hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-opacity-50">
      Calcular
    </button>

    <div v-if="error" class="mt-4 text-red-600 text-sm">
      {{ error }}
    </div>

    <div v-if="results" class="mt-4 space-y-2">
      <p>Suma: <span class="font-semibold">{{ results.suma }}</span></p>
      <p>Resta: <span class="font-semibold">{{ results.resta }}</span></p>
      <p>Multiplicación: <span class="font-semibold">{{ results.multiplicacion }}</span></p>
      <p>División: <span class="font-semibold">{{ results.division }}</span></p>
      <p>Módulo: <span class="font-semibold">{{ results.modulo }}</span></p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

// Se define la estructura esperada de los resultados
interface Results {
  suma: number;
  resta: number;
  multiplicacion: number;
  division: string;
  modulo: number;
}

const num1 = ref<number | null>(null)
const num2 = ref<number | null>(null)
const results = ref<Results | null>(null)
const error = ref<string>('')

// Se genera una funcion para evitar distintos tipos de errores asociados al ingreso de datos
const validaciones = (): boolean => {
  if (num1.value == null || num2.value == null) {
    error.value = "Ingresa un número válido";
    return false;
  }
  else if (num1.value! <= 0 || num2.value! <= 0) {
    error.value = "Ambos números deben ser mayores a cero.";
    return false;
  }
  else if (num1.value === num2.value) {
    error.value = "Ambos números deben ser distintos.";
    return false;
  }
  error.value = "";
  return true;

}
const calcularOperaciones = (): void => {
  results.value = null;
  if (validaciones()) {
    results.value = {
      suma: num1.value! + num2.value!,
      resta: num1.value! - num2.value!,
      multiplicacion: num1.value! * num2.value!,
      division: (num1.value! / num2.value!).toFixed(2), // Limitar a 2 decimales
      modulo: num1.value! % num2.value!,
    };
  }
}
</script>

