<!--事件处理-->
<script setup lang="ts">
import { ref } from 'vue';

const count = ref(0);
const name = ref('Vue.js');
const inputValue = ref('');

function greet(event) {
  alert(`Hello ${name.value}!`);
  // `event` 是 DOM 原生事件
  if (event) {
    alert(event.target.tagName);
  }
}

function say(message) {
  alert(message);
}

function warn(message, event) {
  // 这里可以访问原生事件
  if (event) {
    event.preventDefault();
  }
  alert(message);
}
</script>

<template>
  <!--1.内联事件处理器 处理简单的场景-->
  <h1>Count is {{ count }}</h1>
  <el-button type="primary" @click="count++">Add 1</el-button>
  <el-divider />
  <!--2.方法处理器 处理复杂的场景-->
  <button @click="greet">Greet</button>
  <el-divider />
  <!--3.在内联处理器中调用方法-->
  <el-button @click="say('hello')">Say hello</el-button>
  <el-button @click="say('bye')">Say bye</el-button>
  <el-divider />
  <!--4.在内联事件处理器中访问事件参数-->
  <!--4.1.使用特殊的 $event 变量 -->
  <el-button @click="warn('Form cannot be submitted yet.', $event)">
    Submit
  </el-button>
  <!--4.2.使用内联箭头函数 -->
  <el-button @click="(event) => warn('Form cannot be submitted yet.', event)">
    Submit
  </el-button>
  <el-divider />
  <!--5.按键修饰符-->
  <el-input
    v-model="inputValue"
    @keyup.enter="console.log(inputValue)"
  ></el-input>
  <!--更多的按键修饰符、鼠标修饰符查看官网-->
  <!--6.事件修饰符https://cn.vuejs.org/guide/essentials/event-handling.html#event-modifiers-->
</template>

<style scoped></style>
