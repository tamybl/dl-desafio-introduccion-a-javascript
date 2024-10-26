<script setup>
import { ref } from 'vue';
import OperacionDosNumeros from './components/OperacionDosNumeros.vue'
import ConversorTemperatura from './components/ConversorTemperatura.vue'
import ConvertirDias from './components/ConvertirDias.vue';
import CalcularNumeros from './components/CalcularNumeros.vue';

let currentComponent = ref(0);


const toggleExercise = function(num) {
  currentComponent.value = num;
}

</script>

<template>
  <section class="section__menu">
  <h1>Ejercicios</h1>
  <p>Selecciona una de las opciones:</p>
  <article class="flex w-100">
    <button class="flex-auto" @click="toggleExercise(1)">Reto 1</button>
    <button @click="toggleExercise(2)">Reto 2</button>
    <button @click="toggleExercise(3)">Reto 3</button>
    <button @click="toggleExercise(4)">Reto 4</button>
    <div></div>
  </article>
  </section>
  <section class="section__respuestas">
  <OperacionDosNumeros v-if="currentComponent === 1" />
  <ConversorTemperatura v-if="currentComponent === 2"/>
  <ConvertirDias v-if="currentComponent === 3"/>
  <CalcularNumeros v-if="currentComponent === 4" />
</section>
</template>

<style scoped>
.section__menu article {
    display: flex;
    justify-content: space-around;
    max-width: 600px;
    margin: 0 auto;
    padding: 1rem 0;
}
.section__menu article button {
  width: 100%;
  margin-left: 1rem;
}
.section__respuestas {
  padding: 1.5rem 0;

}
</style>
