<script setup>
import { ref } from 'vue';
import Alerta from './Alerta.vue'


const presupuesto = ref(0)
const error = ref('')



const emit = defineEmits(['definir-presupuesto'])
const definirPresupuesto = ()=>{
    if(presupuesto.value === 0){
        error.value = 'presupuesto no valido!!!';

        setTimeout(()=>{
            error.value = ''
        },3000)
    }

    emit('definir-presupuesto', presupuesto.value)

    return

    
}


</script>
<template>
    <div class="flex justify-center mt-4">
        <form 
            class="flex flex-col items-center gap-1 mt-4"
            @submit.prevent="definirPresupuesto"
        
        >
            <Alerta v-if="error">
                {{ error }}
            </Alerta>
            <label for="presupuesto" class="font-semibold">Define el Presupuesto: </label>
            <input 
                id="presupuesto"
                type="number"
                placeholder="define el presupuesto"
                min="0"                
                v-model.number="presupuesto"
                class="border-none rounded-md text-gray-950 text-center font-medium"    
            >
            <input 
                type="submit"
                value="Definir Presupuesto"
                class="bg-green-600 mt-4 w-full rounded-md font-semibold cursor-pointer hover:bg-green-700 transition-colors"    
            >
        </form>
    </div>
</template>
