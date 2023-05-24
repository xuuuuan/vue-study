<script setup lang="ts">
import { ref } from 'vue';

const greetingMessage = ref('hello world');
</script>

<template>
  <div>
    <!--可以像对组件传递 props 那样，向一个插槽的出口上传递 attributes：-->
    <slot :text="greetingMessage" :count="1" />
  </div>
</template>

<style scoped></style>
