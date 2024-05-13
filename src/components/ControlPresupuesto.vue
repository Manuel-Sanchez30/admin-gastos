<script setup>

import imgLogo from '../assets/vue.svg'
import {formatearCantidad} from '../helpers'

const props = defineProps({
    presupuesto:{
        type:Number,
        required:true,
    },
    disponible:{
        type:Number,
        required:true,
    }
})

</script>

<template>
    <div class="flex flex-col items-center mt-10 gap-5 ">        

        <div class="flex flex-col items-center gap-4 sm:flex-row sm:gap-10">
            <div>
                <img :src="imgLogo" alt="">
            </div>
            <div class="flex flex-col items-center gap-4">
                <div class="font-semibold">
                    <p>Presupuesto: {{ formatearCantidad(presupuesto) }}</p>
                    <p>Disponible: {{ formatearCantidad(disponible) }}</p>
                    <p>Gastado: $0</p>
                </div>
                <input 
                    type="button"
                    value="Resetear App"
                    class="bg-rose-600 w-40 rounded-md font-semibold cursor-pointer hover:bg-rose-700 transition-colors"    
                > 
            </div>
            
        </div>
        
    </div>
</template>
