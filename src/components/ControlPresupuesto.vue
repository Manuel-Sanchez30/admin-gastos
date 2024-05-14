<script setup>
import CircleProgress from 'vue3-circle-progress'
import 'vue3-circle-progress/dist/circle-progress.css'    
import {formatearCantidad} from '../helpers'
import { computed } from 'vue';

defineEmits(['resetear-app'])

const props = defineProps({
    presupuesto:{
        type:Number,
        required:true,
    },
    disponible:{
        type:Number,
        required:true,
    },
    gastado:{
        type:Number,
        required:true
    }
})

const porcentaje = computed(()=>{    
    return parseInt( ((props.presupuesto - props.disponible) / props.presupuesto) * 100 )
});

</script>

<template>
    <div class="flex flex-col items-center mt-10 gap-5 ">        

        <div class="flex flex-col items-center gap-4 sm:flex-row sm:gap-10">
            <div class="relative">
                <p class="absolute m-auto left-0 right-0 text-center z-10 text-xl font-bold text-white top-1/3">{{ porcentaje }}%</p>

                <CircleProgress
                    :percent="porcentaje"
                    :size="100"
                    :border-width="15"
                    :border-bg-width="15"
                    fill-color="#4F46E5"
                    empty-color="#e1e1e1"
                />
            </div>
            <div class="flex flex-col items-center gap-4">
                <div class="font-semibold">
                    <p>Presupuesto: {{ formatearCantidad(presupuesto) }}</p>
                    <p>Disponible: {{ formatearCantidad(disponible) }}</p>
                    <p>Gastado: {{ formatearCantidad(gastado) }}</p>
                </div>
                <button
                    @click="$emit('resetear-app')"
                    class="bg-rose-600 w-40 rounded-md font-semibold cursor-pointer hover:bg-rose-700 transition-colors"
                >
                    Resetear App
                    
                </button> 
                
            </div>
            
        </div>
        
    </div>
</template>
