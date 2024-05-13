<script setup>

    import imgClose from '../assets/img/close_10238407 (1).png'

    defineEmits(['cerrar-modal'])

</script>

<template>
    <div class="absolute top-0 right-0 left-0 bottom-0 bg-slate-950/80 text-">
        <div>
            <img 
                :src="imgClose"
                alt="img-close"
                class="w-6 right-8 top-8 cursor-pointer absolute"
                @click="$emit('cerrar-modal')"    
            >
        </div>
        <form class="flex flex-col items-center mt-32 mr-auto mb-0 ml-auto w-11/12">
            <legend class="text-2xl font-semibold mb-6">Añadir Gasto</legend>
            <div class="mb-2">
                <label for="nombre" class="font-semibold block">Nombre: </label>
                <input 
                    type="text"
                    id="nombre"
                    placeholder="Nombre del Gasto"
                    class="rounded-md p-1 w-72 font-semibold text-gray-900"
                >
            </div>
            <div class="mb-2">
                <label for="cantidad" class="font-semibold block">Cantidad: </label>
                <input 
                    type="number"
                    id="cantidad"
                    placeholder="Ingresa la Cantidad"
                    class="rounded-md p-1 w-72 font-semibold text-gray-900"
                >
            </div>
            <div class="mb-2">
                <label for="categoria" class="font-semibold block">Categoria: </label>
                <select 
                    name="categoria"
                    id="categoria"
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
                value="Añadir Gasto"
                class="bg-indigo-600 w-72 rounded-md font-semibold cursor-pointer hover:bg-indigo-700 transition-colors"    
            >
        </form>
    </div>
</template>



