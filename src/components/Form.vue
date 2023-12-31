<script setup lang="ts">
import { reactive } from 'vue';
import Alert from './Alert.vue';
//import { Patient } from '../entities/patient';

const alerta = reactive({
  type: '',
  message: '',
});


const emit = defineEmits([
  'update:name',
  'update:email',
  'update:owner',
  'update:sintomas',
  'update:alta',
  'save-patient',
]);

const props = defineProps<{
  name: '';
  owner: '';
  email: '';
  alta: '';
  sintomas: '';
}>();
const validate = () => {
  if (Object.values(props).includes('')) {
    alerta.message = 'Todos os campos são obrigatórios';
    alerta.type = 'error';
    return;
  }
  emit('save-patient');
  alerta.message = 'Guardado correctamente';
  alerta.type = 'success';
  setTimeout(() => {
    Object.assign(alerta, {
      type: '',
      message: '',
    });
  }, 2000);
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
          :value="name"
          @input="$emit('update:name', $event.target?.value)"
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
          :value="owner"
          @input="$emit('update:owner', $event.target?.value)"
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
          :value="email"
          @input="$emit('update:email', $event.target?.value)"
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
          :value="alta"
          @input="$emit('update:alta', $event.target?.value)"
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
          :value="sintomas"
          @input="$emit('update:sintomas', $event.target?.value)"
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
