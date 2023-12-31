<script setup lang="ts">
import Header from './components/Header.vue';
import Form from './components/Form.vue';
import { ref, reactive } from 'vue';
import { Patient as PatientProps } from './entities/patient';
import Patient from './components/Patient.vue';

const patients = ref<PatientProps[]>([]);

const patient = reactive({
  id: null,
  name: '',
  owner: '',
  email: '',
  alta: '',
  sintomas: '',
});

const savePatient = () => {
  if (patient.id) {
    const {id} = patient
    const index = patients.value.findIndex(p => p.id === id)
    patients.value[index] = {...patient}
  } else {
    patients.value.push({ ...patient, id: new Date().getUTCMilliseconds() });
  }
  Object.assign(patient, {
    name: '',
    owner: '',
    email: '',
    alta: '',
    sintomas: '',
    id: null
  });
};

const editPatient = (id: number) => {
  const patientEdit = patients.value.filter((p) => p.id === id)[0];
  Object.assign(patient, patientEdit);
};
</script>

<template>
  <div class="container mx-auto mt-8">
    <Header />
    <div class="mt-12 md:flex">
      <Form
        v-model:name="patient.name"
        v-model:owner="patient.owner"
        v-model:email="patient.email"
        v-model:alta="patient.alta"
        v-model:sintomas="patient.sintomas"
        @save-patient="savePatient"
        :id="patient.id"
      />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Admin your patient</h3>
        <div v-if="patients.length > 0">
          <p class="text-lg text-center mt-5 mb-10">
            Informações de
            <span class="text-indigo-600 font-bold">Pacientes</span>
          </p>
          <Patient
            v-for="patient in patients"
            :patient="patient"
            @edit-patient="editPatient"
          />
        </div>
        <p v-else class="mt-20 text-2xl text-center text-red-500">
          Sem pacientes
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
