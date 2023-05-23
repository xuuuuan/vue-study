<script setup lang="ts">
defineProps<{
  step: number;
}>();

defineEmits<{
  (event: 'increaseBy', num: number): void;
}>();
</script>

<template>
  <el-button @click="$emit('increaseBy', step)" type="primary">click</el-button>
</template>

<style scoped></style>
