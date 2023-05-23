<script setup lang="ts">
defineProps<{
  firstName: string;
  lastName: string;
}>();

defineEmits<{
  (event: 'update:firstName', value: string): void;
  (event: 'update:lastName', value: string): void;
}>();
</script>

<template>
  <input
    type="text"
    :value="firstName"
    @input="$emit('update:firstName', $event.target.value)"
  />
  <input
    type="text"
    :value="lastName"
    @input="$emit('update:lastName', $event.target.value)"
  />
</template>

<style scoped></style>
