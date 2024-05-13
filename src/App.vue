<script setup>

import { ref } from 'vue';
import ControlPresupuesto from './components/ControlPresupuesto.vue';
import Presupuesto from './components/Presupuesto.vue';
import imgPlus from './assets/img/plus_10024172.png'




const presupuesto = ref(0)
const disponible = ref(0)

const definirPresupuesto = (cantidad)=>{
  presupuesto.value = cantidad
  disponible.value = cantidad
}

const modal = ()=>{
  console.log('diste click');
}

</script>

<template>
  <div class="container mx-auto">
    <header>
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
    </header>
    <main v-if="presupuesto > 0">
      <div >
        <img 
          :src="imgPlus"
          alt="img-plus"
          class="fixed w-8 cursor-pointer right-12 bottom-1"  
        >
        
      </div>
    </main>
    
  </div>
</template>

