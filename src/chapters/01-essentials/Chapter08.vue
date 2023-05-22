<!--模板引用-->
<!--虽然 Vue 的声明性渲染模型为你抽象了大部分对 DOM 的直接操作，
但在某些情况下，我们仍然需要直接访问底层 DOM 元素。
要实现这一点，我们可以使用特殊的 ref attribute-->
<script setup lang="ts">
import { ref, watchEffect } from 'vue';
// 1.访问模板引用
const input = ref(null);
const inputValue = ref('');
// 注意，只可以在组件挂载后才能访问模板引用。
// 如果你想在模板中的表达式上访问 input，在初次渲染时会是 null。
// 这是因为在初次渲染前这个元素还不存在呢！
// 如果你需要侦听一个模板引用 ref 的变化，确保考虑到其值为 null 的情况：
watchEffect(() => {
  // 达到的效果是组件挂在完毕就focus到input框
  if (input.value !== null) {
    input.value.focus();
  } else {
    // 此时还未挂载，或此元素已经被卸载（例如通过 v-if 控制）
  }
});

// 2.v-for 中的模板引用
const list = ref(['a', 'b', 'c']);
const itemRefs = ref([]);
</script>

<template>
  <!--1.访问模板引用-->
  <el-input ref="input" v-model="inputValue" placeholder="Please input" />
  <el-button type="primary" @click="input.focus()">Focus the input</el-button>
  <el-divider />
  <!--2.v-for 中的模板引用-->
  <ul>
    <li v-for="item in list" ref="itemRefs">
      {{ item }}
    </li>
  </ul>
  <!--itemRefs 是DOM li的集合-->
  <el-button
    type="primary"
    @click="itemRefs.map((item) => console.log(item.textContent))"
    >Print values
  </el-button>
  <el-divider />
  <!--3.函数模板引用-->
  <!--除了使用字符串值作名字，ref attribute 还可以绑定为一个函数，会在每次组件更新时都被调用。
  该函数会收到元素引用作为其第一个参数。注意我们这里需要使用动态的 :ref 绑定才能够传入一个函数。
  当绑定的元素被卸载时，函数也会被调用一次，此时的 el 参数会是 null。当然也可以绑定一个组件方法而不是内联函数-->
  <input :ref="(el) => { /* 将 el 赋值给一个数据属性或 ref 变量 */ console.log(el) }">

  <!--4.组件上的 ref TODO 了解组件的知识再跳回来看-->
</template>

<style scoped></style>
