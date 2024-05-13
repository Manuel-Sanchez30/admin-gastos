<script setup>

import { ref } from 'vue';
import ControlPresupuesto from './components/ControlPresupuesto.vue';
import Presupuesto from './components/Presupuesto.vue';

const presupuesto = ref(0)
const disponible = ref(0)

const definirPresupuesto = (cantidad)=>{
  presupuesto.value = cantidad
  disponible.value = cantidad
}

</script>

<template>
  <div class="container mx-auto">
    <h1 class="text-4xl text-center font-bold text-indigo-700 mt-8">Planificador de Gastos</h1>

    <div>
      <Presupuesto
        v-if="presupuesto === 0"
        @definir-presupuesto="definirPresupuesto"
      />
      <ControlPresupuesto
        v-else
        :presupuesto="presupuesto"
        :disponible="disponible"
      />

    </div>
  </div>
</template>

