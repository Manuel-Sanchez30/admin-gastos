<script setup>

//sintaxis corta para recibir las props
defineProps(['filtro'])
defineEmits(['update:filtro'])

</script>
<template>
    <div>
        <form class="flex flex-col mt-4 items-center sm:flex-row sm:justify-center sm:gap-4 ">
            <label 
                for="filtro"
                class="font-semibold mb-2 sm:text-2xl sm:mt-4"    
            >Filtrar Gastos</label>
            <select 
                    name="categoria"
                    id="filtro"
                    :value="filtro"
                    @input="$emit('update:filtro', $event.target.value)"
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
        </form>
    </div>
</template>



