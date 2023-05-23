<script setup lang="ts">
const props = defineProps<{
  title: string;
  content: string;
}>();

// 不能这样做 错误的
// props.content = 'ss';
</script>

<template>

</template>

<style scoped>

</style>