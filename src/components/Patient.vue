<script setup lang="ts">
import {Patient} from '../entities/patient.ts'
defineProps<{
  patient: Patient;
}>();

</script>
<template>
    <div class="mx-5 mt-10 bg-white shadow-md px-5 py-10 rounded-xl">
        <p class="font-bold mb-3 text-gray-700 uppercase">
            <span class="font-normal normal-case"></span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Id:
            <span class="font-normal normal-case">{{ patient.id }}</span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Name:
            <span class="font-normal normal-case">{{ patient.name }}</span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Owner: 
            <span class="font-normal normal-case">{{ patient.owner }}</span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">E-mail: 
            <span class="font-normal normal-case">{{ patient.email }}</span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Data de Alta: 
            <span class="font-normal normal-case">{{ patient.alta }}</span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Sintomas: 
            <span class="font-normal normal-case">{{ patient.sintomas }}</span>
        </p>
        <div class="grid md:grid-cols-2 gap-5 mt-10">
            <button type="button" class="block w-full 
            py-2 px-10 bg-indigo-700 text-white font-bold uppercase rounded-lg">
        Editar</button>
            <button type="button" class="block w-full 
            py-2 px-10 bg-red-600 text-white font-bold uppercase rounded-lg">
        Eliminar</button>
        </div>
    </div>
</template>