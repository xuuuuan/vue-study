<!--监听器-->
<script setup lang="ts">
import { reactive, ref, watch, watchEffect } from 'vue';

const question = ref('');
const answer = ref('I cannot give you an answer until you ask a question!');

// 1.基本实例
watch(question, async (newQuestion) => {
  if (newQuestion.indexOf('?') > -1) {
    answer.value = 'Thinking...';
    try {
      const res = await fetch('https://yesno.wtf/api');
      answer.value = (await res.json()).answer;
    } catch (error) {
      answer.value = 'Error! Could not reach the API. ' + error;
    }
  }
});

// 2.数据类型
// watch 的第一个参数可以是不同形式的“数据源”：
// 它可以是一个 ref (包括计算属性)、一个响应式对象、一个 getter 函数、或多个数据源组成的数组
const x = ref(0);
const y = ref(0);

// 单个 ref
watch(x, (newX) => {
  console.log(`x is ${newX}`);
});

// getter 函数
watch(
  () => x.value + y.value,
  (sum) => {
    console.log(`sum of x + y is: ${sum}`);
  },
);

// 多个来源组成的数组
watch([x, () => y.value], ([newX, newY]) => {
  console.log(`x is ${newX} and y is ${newY}`);
});
// 注意，你不能直接侦听响应式对象的属性值。 需要使用getter
const obj = reactive({ count: 0 });
// 错误，因为 watch() 得到的参数是一个 number
// watch(obj.count, (count) => {
//   console.log(`count is: ${count}`)
// })
// 提供一个 getter 函数
watch(
  () => obj.count,
  (count) => {
    console.log(`count is: ${count}`);
  },
);

// 3.深层侦听器 这个不是很理解 继续看官网

// 4.即时回调的侦听器
// watch 默认是懒执行的：仅当数据源变化时，才会执行回调。
// 但在某些场景中，我们希望在创建侦听器时，立即执行一遍回调。
// 举例来说，我们想请求一些初始数据，然后在相关状态更改时重新请求数据。
// 我们可以通过传入 immediate: true 选项来强制侦听器的回调立即执行
const source = ref('');
watch(
  source,
  (newValue, oldValue) => {
    // 立即执行，且当 `source` 改变时再次执行
  },
  { immediate: true },
);

// 5.watchEffect()
// watchEffect() 会立即执行传入的函数，并响应式追踪其依赖，并在其依赖变更时重新运行该函数。
// 与 watch() 不同的是，它不接受一个要侦听的特定源响应式对象。
// 一个常见的使用场景是需要在组件上下文之外执行副作用函数的情况。
const todoId = ref(1);
const data = ref(null);
/*watch(
  todoId,
  async () => {
    const response = await fetch(
      `https://jsonplaceholder.typicode.com/todos/${todoId.value}`,
    );
    data.value = await response.json();
  },
  { immediate: true },
);*/
// 我们可以用 watchEffect 函数 来简化上面的代码。
// watchEffect() 允许我们自动跟踪回调的响应式依赖
watchEffect(async () => {
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`,
  );
  data.value = await response.json();
  console.log(data.value);
});

// 6.回调的触发时机、停止侦听器查看官网
// https://cn.vuejs.org/guide/essentials/watchers.html
</script>

<template>
  <p>
    Ask a yes/no question:
    <input v-model="question" />
  </p>
  <p>{{ answer }}</p>
  <el-divider />
  <el-input v-model="todoId"></el-input>
</template>

<style scoped></style>
