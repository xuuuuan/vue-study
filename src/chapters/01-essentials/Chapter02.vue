<!--
Chapter02 计算属性
计算属性缓存 vs 方法
  若我们将同样的函数定义为一个方法而不是计算属性，两种方式在结果上确实是完全相同的，
  然而，不同之处在于计算属性值会基于其响应式依赖被缓存。
  一个计算属性仅会在其响应式依赖更新时才重新计算。
  这意味着只要 author.books 不改变，无论多少次访问 publishedBooksMessage 都会立即返回先前的计算结果
-->

<script setup lang="ts">
import { computed, ref } from 'vue';

const author = ref({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery',
  ],
});

// 一个计算属性 ref
const publishedBooksMessage = computed(() => {
  return author.value.books.length > 0 ? 'Yes' : 'No';
});

// 计算属性默认是只读的。当你尝试修改一个计算属性时，你会收到一个运行时警告。
// 只在某些特殊场景中你可能才需要用到“可写”的属性，你可以通过同时提供 getter 和 setter 来创建
const firstName = ref('John');
const lastName = ref('Doe');

const fullName = computed({
  // getter
  get: () => {
    return `${firstName.value} ${lastName.value}`;
  },
  // setter
  set: (value) => {
    // 注意：我们这里使用的是解构赋值语法
    [firstName.value, lastName.value] = value.split(' ');
  },
});
</script>

<template>
  <p>Has published books:</p>
  <span>{{ publishedBooksMessage }}</span>
  <p>Full name:</p>
  <span>{{ fullName }}</span>
  <el-input v-model="fullName" placeholder="Please input your name" />
</template>
