<script setup>
import { ref,reactive, watch, computed } from 'vue';


import ControlPresupuesto from './components/ControlPresupuesto.vue';
import Presupuesto from './components/Presupuesto.vue';
import Modal from './components/Modal.vue'
import Gasto from './components/Gasto.vue'
import { generarId } from './helpers';
import imgPlus from './assets/img/plus_10024172.png'
import Filtro from './components/Filtro.vue';


const presupuesto = ref(0);
const disponible = ref(0);
const gastos = ref([]);
const gastado = ref(0);
const filtro = ref('');

const gasto = reactive({
  nombre:'',
  cantidad:'',
  categoria:'',
  id:null,
  fecha: Date.now()
})

const modal = reactive({
  mostrar:false
})

const definirPresupuesto = (cantidad)=>{
  presupuesto.value = cantidad
  disponible.value = cantidad
}

watch(gastos,()=>{
  const totalGastado = gastos.value.reduce((total,gasto) => gasto.cantidad + total, 0)
  gastado.value = totalGastado
  disponible.value = presupuesto.value - totalGastado
},{
  deep:true,
});

watch(modal,()=>{
  if(!modal.mostrar){
    reiniciarStateGasto()
  }
},
{
  deep:true,
});

const mostrarModal = ()=>{
  modal.mostrar = true;
}

const cerrarModal = ()=>{
  modal.mostrar = false;
  
}

const guardarGasto = ()=>{
  //evitar resgistros duplicados
  if(gasto.id){
    const {id} = gasto
    const index = gastos.value.findIndex(gasto => gasto.id === id)
    gastos.value[index] = {...gasto}

  }else{
      gastos.value.push({
      ...gasto,
      id:generarId()
    })
  }  

  cerrarModal()

  reiniciarStateGasto()

}
//reiniciar state de Gasto
const reiniciarStateGasto = ()=>{
  Object.assign(gasto,{
    nombre:'',
    cantidad:'',
    categoria:'',
    id:null,
    fecha: Date.now()
  })
}

//editar Gasto
const seleccionarGasto = (id)=>{
  const gastoEditar = gastos.value.filter(gasto => gasto.id === id)[0]
  Object.assign(gasto,gastoEditar)
  mostrarModal()
}

//eliminar gasto
const eliminarGasto = ()=>{
  
  if(confirm('Eliminar Gasto?')){
    gastos.value = gastos.value.filter(gastoState => gastoState.id !== gasto.id)
    cerrarModal()
  }
    
}

//filtrar gastos
const gastosFiltrados = computed(()=>{
  if(filtro.value){
    return gastos.value.filter(gasto => gasto.categoria === filtro.value)
  }
  return gastos.value
})



</script>

<template>
  <div 
    class="container mx-auto"
    :class="[modal.mostrar ? 'overflow-hidden max-h-screen' : '']"  
  >
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
          :gastado="gastado"
        />

      </div>
    </header>
    <main v-if="presupuesto > 0">

      <Filtro
        v-model:filtro="filtro"
      />

      <div>
        <h2 
          class="mt-5 text-center font-semibold text-2xl"
        >
          {{ gastosFiltrados.length > 0 ? 'Gastos' : 'No hay Gastos' }}
        </h2>

      <Gasto
        v-for="gasto in gastosFiltrados"
        :key="gasto.id"
        :gasto="gasto"
        @seleccionar-gasto="seleccionarGasto"
      />
      </div>
      

      <div >
        <img 
          :src="imgPlus"
          alt="img-plus"
          class="fixed w-8 cursor-pointer right-8 bottom-1"
          @click="mostrarModal"  
        >
        <Modal
          v-if="modal.mostrar"
          :disponible="disponible"
          :id="gasto.id"
          @cerrar-modal="cerrarModal"
          @guardar-gasto="guardarGasto"
          @eliminar-gasto="eliminarGasto"
          v-model:nombre="gasto.nombre"
          v-model:cantidad="gasto.cantidad"
          v-model:categoria="gasto.categoria"

        />
      </div>
    </main>
    
  </div>
</template>

