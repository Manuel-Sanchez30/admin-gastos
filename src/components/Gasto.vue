<script setup>
import { formatearCantidad, formatearFecha } from '../helpers';
import IconoAhorro from '../assets/img/icono_ahorro.svg'
import IconoCasa from '../assets/img/icono_casa.svg'
import IconoComida from '../assets/img/icono_comida.svg'
import IconoGastos from '../assets/img/icono_gastos.svg'
import IconoOcio from '../assets/img/icono_ocio.svg'
import IconoSalud from '../assets/img/icono_salud.svg'
import IconoSuscripciones from '../assets/img/icono_suscripciones.svg'


const props = defineProps({
    gasto:{
        type:Object,
        required:true,
    }
})

defineEmits(['seleccionar-gasto'])

//diccionario para renderizar los iconos segun la categoria
const diccionarioIconos = {
    ahorro:IconoAhorro,
    comida:IconoComida,
    casa:IconoCasa,
    gastos:IconoGastos,
    ocio:IconoOcio,
    salud:IconoSalud,
    suscripciones:IconoSuscripciones
}

</script>

<template>
    <div class="flex justify-between items-center mt-8 ml-4 mr-4 sm:justify-evenly shadow-indigo-600/10 shadow-lg">
        <div class="flex items-center gap-4">
            <div>
                <img 
                    :src="diccionarioIconos[gasto.categoria]"
                    alt="icono-gasto"
                    class="w-10"    
                >
            </div>
            <div>
                <p class="uppercase font-semibold text-indigo-600">{{ gasto.categoria }}</p>
                <p 
                    class="cursor-pointer hover:font-semibold"
                    @click="$emit('seleccionar-gasto', gasto.id)"    
                >{{ gasto.nombre }}</p>
                <p>{{ formatearFecha(gasto.fecha) }}</p>
            </div>
        </div>
        
        <p class="font-semibold text-lg">{{ formatearCantidad(gasto.cantidad) }}</p>
    </div>
</template>


