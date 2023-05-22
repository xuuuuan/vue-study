<script setup lang="ts">
import { ref } from 'vue';

const count = ref(0);
</script>

<template>
  <el-button type="primary" @click="count++">
    You clicked me {{ count }} times.
  </el-button>
</template>

<style scoped></style>
