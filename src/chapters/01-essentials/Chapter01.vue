<!--
Chapter01 模板语法、响应式基础
响应式API 我本人更倾向于用ref()
-->

<script setup lang="ts">
import { ref } from 'vue';

interface User {
  name: string;
  age: number;
}

const user = ref<User>({
  name: 'John Doe',
  age: 18,
});

const count = ref(0);

console.log(count); // { value: 0 }
console.log(count.value); // 0

count.value++;
console.log(count.value); // 1

user.value = {
  name: 'Mars',
  age: 19,
};

function increment() {
  count.value++;
}
</script>

<template>
  <div class="user">
    <h3>{{ user.name }}</h3>
    <p>Age: {{ user.age }}</p>
  </div>
  <div>{{ count }}</div>
  <el-button type="primary" @click="increment">click</el-button>
</template>

<style scoped></style>
