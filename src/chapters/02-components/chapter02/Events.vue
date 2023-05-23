<!--组件事件-->
<!--此章节可查看官网https://cn.vuejs.org/guide/components/events.html-->
<script setup lang="ts">
import IncreaseButton from '@/chapters/02-components/chapter02/IncreaseButton.vue';
import { ref } from 'vue';

const count = ref(0);
</script>

<template>
  <h1>{{ count }}</h1>
  <IncreaseButton
    :step="5"
    @increase-by="
      (num) => {
        count += num;
      }
    "
  />
</template>

<style scoped></style>
