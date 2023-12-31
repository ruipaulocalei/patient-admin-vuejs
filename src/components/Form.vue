<script setup lang="ts">
import { reactive } from 'vue';
import Alert from './Alert.vue'

const alerta = reactive({
    type: '',
    message: '',
})
const paciente = reactive({
  name: '',
  owner: '',
  email: '',
  alta: '',
  sintomas: '',
});

const validate = () => {
  if (Object.values(paciente).includes('')) {
    alerta.message = 'Todos os campos são obrigatórios'
    alerta.type = 'error'
    console.log('error')
    return;
  }
  alerta.message = 'Guardado correctamente'
  alerta.type = 'success'
};
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center">Seguimento de Pacientes</h2>
    <p class="text-lg text-center mt-5 mb-10">
      Adiciona Pacientes e
      <span class="text-indigo-600 font-bold">Administra-os</span>
    </p>
    <Alert v-if="alerta.message" :alerta="alerta" />
    <form
      class="bg-white shadow-md rounded-lg py-10 px-5 mb-10 space-y-5"
      @submit.prevent="validate"
    >
      <div class="">
        <label for="name" class="block text-gray-700 uppercase font-bold"
          >Nome do animal</label
        >
        <input
          type="text"
          id="name"
          class="border-2 w-full p-2 mt-2 placeholder-gray-500 rounded-md"
          placeholder="Nome do animal"
          v-model="paciente.name"
        />
      </div>
      <div class="">
        <label for="owner" class="block text-gray-700 uppercase font-bold"
          >Nome do proprietário</label
        >
        <input
          type="text"
          id="owner"
          class="border-2 w-full p-2 mt-2 placeholder-gray-500 rounded-md"
          placeholder="Nome do proprietário"
          v-model="paciente.owner"
        />
      </div>
      <div class="">
        <label for="email" class="block text-gray-700 uppercase font-bold"
          >E-mail</label
        >
        <input
          type="email"
          id="email"
          class="border-2 w-full p-2 mt-2 placeholder-gray-500 rounded-md"
          placeholder="E-mail do proprietário"
          v-model="paciente.email"
        />
      </div>
      <div class="">
        <label for="alta" class="block text-gray-700 uppercase font-bold"
          >Alta</label
        >
        <input
          type="date"
          id="alta"
          class="border-2 w-full p-2 mt-2 placeholder-gray-500 rounded-md"
          v-model="paciente.alta"
        />
      </div>
      <div class="">
        <label for="sintomas" class="block text-gray-700 uppercase font-bold"
          >Sintomas</label
        >
        <textarea
          id="sintomas"
          class="border-2 w-full p-2 mt-2 placeholder-gray-500 rounded-md h-40"
          placeholder="Descreva os sintomas"
          v-model="paciente.sintomas"
        />
      </div>
      <input
        type="submit"
        value="Registrar Paciente"
        class="bg-indigo-600 w-full uppercase font-bold p-3 text-white hover:bg-indigo-800 cursor-pointer transition-colors"
      />
    </form>
  </div>
</template>
