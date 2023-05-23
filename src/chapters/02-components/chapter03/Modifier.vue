<script setup lang="ts">
const props = defineProps<{
  text: string;
  textModifiers: {
    default: () => void;
    upper: () => void;
    lower: () => void;
  };
}>();

const emit = defineEmits<{
  (event: 'update:text', value: string): void;
}>();

function emitText(e) {
  let value = e.target.value;
  if (props.textModifiers.upper) {
    value = value.toUpperCase();
  } else if (props.textModifiers.lower) {
    value = value.toLowerCase();
  }
  emit('update:text', value);
}
</script>

<template>
  <input :value="text" @input="emitText" />
</template>

<style scoped></style>
