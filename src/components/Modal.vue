<script setup>
    import { ref, computed } from 'vue';
    import Alerta from './Alerta.vue';

    import imgClose from '../assets/img/close_10238407 (1).png'

    const error = ref('')

    const props = defineProps({
        nombre:{
            type:String,
            required:true,
        },
        cantidad:{
            type:[String, Number],
            required:true,
        },
        categoria:{
            type:String,
            required:true,
        },
        disponible:{
            type:Number,
            required:true
        },
        id:{
            type:[String, null],
            required:true
        }
    })

    const cambiarText = computed(()=>{
        return props.id
    })

    const emit = defineEmits(['cerrar-modal','guardar-gasto','eliminar-gasto', 'update:nombre', 'update:cantidad', 'update:categoria'])

    const old = props.cantidad

    const agregarGasto = ()=>{
        const {nombre,cantidad,categoria, disponible, id} = props

        //validar que todos los campos sean obligatorios
        if([nombre,cantidad,categoria].includes('')){
            error.value = 'Todos los campos son obligatorios'

            setTimeout(()=>{
                error.value = ''
            },3000)
            
            return
        }

        if(id){
            //validar cantidad no exceda el disponible
            if(cantidad > old + disponible){
                error.value = 'Haz excedido el presupuesto'
                setTimeout(()=>{
                    
                },3000)
            
                return
            }
        }else{
            //validar qu la cantidad no sea menor a cero
            if(cantidad <= 0){
                error.value = 'Cantidad no Valida!'

                setTimeout(()=>{
                    error.value = ''
                },3000)

                return
            }
        }
        

        if(cantidad > disponible){
            error.value = 'Excediste el valor Disponible'
            setTimeout(()=>{
                error.value = ''
            },3000)

            return
        }

        emit('guardar-gasto')
    }

</script>

<template>
    <div class="absolute top-0 right-0 left-0 bottom-0 bg-slate-950/80 flex flex-col justify-center items-center z-50">
        <div>
            <img 
                :src="imgClose"
                alt="img-close"
                class="w-6 right-8 top-8 cursor-pointer absolute"
                @click="$emit('cerrar-modal')"    
            >
        </div>
        <form 
            class="flex flex-col items-center mr-auto mb-0 ml-auto w-11/12"
            @submit.prevent="agregarGasto"    
        >
            <legend 
                class="text-2xl font-semibold mb-6"
            >{{ cambiarText ? 'Guardar Cambios' : 'Añadir Gasto' }}</legend>
            <Alerta v-if="error">
                {{ error }}
            </Alerta>
            <div class="mb-2">
                <label for="nombre" class="font-semibold block">Nombre: </label>
                <input 
                    type="text"
                    id="nombre"
                    placeholder="Nombre del Gasto"
                    :value="nombre"
                    @input="$emit('update:nombre', $event.target.value)"
                    class="rounded-md p-1 w-72 font-semibold text-gray-900"
                >
            </div>
            <div class="mb-2">
                <label for="cantidad" class="font-semibold block">Cantidad: </label>
                <input 
                    type="number"
                    id="cantidad"
                    :value="cantidad"
                    @input="$emit('update:cantidad', +$event.target.value)"
                    placeholder="Ingresa la Cantidad"
                    class="rounded-md p-1 w-72 font-semibold text-gray-900"
                >
            </div>
            <div class="mb-2">
                <label for="categoria" class="font-semibold block">Categoria: </label>
                <select 
                    name="categoria"
                    id="categoria"
                    :value="categoria"
                    @input="$emit('update:categoria', $event.target.value)"
                    class="rounded-md p-1 w-72 font-semibold text-gray-900"
                >
                <option value="">--Seleccione--</option>
                <option value="ahorro">Ahorro</option>
                <option value="comida">Comida</option>
                <option value="casa">Casa</option>
                <option value="gastos">Gastos Varios</option>
                <option value="ocio">Ocio</option>
                <option value="salud">Salud</option>
                <option value="suscripciones">Suscripciones</option>
            </select>
            </div>
            <input 
                type="submit"
                :value="[cambiarText ? 'Guardar Cambios' : 'Añadir Gasto']"
                class="bg-indigo-600 w-72 rounded-md font-semibold cursor-pointer hover:bg-indigo-700 transition-colors"    
            >
        </form>
        <button 
            type="button"
            v-if="cambiarText"
            @click="$emit('eliminar-gasto')"
            class="bg-rose-600 rounded-md w-72 mt-8 font-semibold cursor-pointer hover:bg-rose-700 transition-colors "
        >
            Eliminar Gasto
        </button>
    </div>


</template>





