<script setup>
import { ref } from 'vue';
import Presupuesto from './components/Presupuesto.vue';

const presupuesto = ref(0)
</script>

<template>
  <div class="container mx-auto">
    <h1 class="text-4xl text-center font-bold text-indigo-700 mt-8">Planificador de Gastos</h1>
    <div>
      <Presupuesto
        v-model:presupuesto="presupuesto"
      />
    </div>
  </div>
</template>

