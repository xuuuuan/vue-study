<script setup lang="ts">
// 定义props
defineProps<{
  title: string;
  content: string;
}>();
// 定义emits 监听事件
defineEmits<{
  (event: 'enlarge-text'): void;
  (event: 'reduce-text'): void;
}>();
</script>

<template>
  <div>
    <h3>{{ title }}</h3>
    <h4>{{ content }}</h4>
    <el-button @click="$emit('enlarge-text')">Enlarge text</el-button>
    <el-button @click="$emit('reduce-text')">Reduce text</el-button>
  </div>
</template>

<style scoped></style>
