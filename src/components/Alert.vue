<script setup lang="ts">
import { AlertProps } from '../entities/alert';
import { computed } from 'vue';
const props = defineProps<{
  alerta: AlertProps;
}>();

const hasError = computed(() => {
    return props.alerta.type === 'error'
});
</script>
<template>
  <div
    :class="[hasError ? 'bg-red-500':'bg-green-500']"
    class="text-white text-center font-bold rounded-md uppercase p-3 mb-3"
  >
    {{ alerta.message }}
  </div>
</template>
