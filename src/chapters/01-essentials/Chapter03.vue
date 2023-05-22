<!--条件渲染v-if、列表渲染v-for-->
<script setup lang="ts">
import { reactive, ref } from 'vue';

const flag = ref(true);
const type = ref('A');

const parentMessage = ref('Parent');
const items = ref([{ message: 'Foo' }, { message: 'Bar' }]);

const myObject = reactive({
  title: 'How to do lists in Vue',
  author: 'Jane Doe',
  publishedAt: '2016-04-10',
});
</script>

<template>
  <!--条件渲染-->
  <el-button @click="flag = !flag">toggle</el-button>
  <h1 v-if="flag">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>

  <div v-if="type === 'A'">A</div>
  <div v-else-if="type === 'B'">B</div>
  <div v-else-if="type === 'C'">C</div>
  <div v-else>Not A/B/C</div>

  <h1 v-show="flag">Hello!</h1>
  <!--v-if 和 v-show的区别-->
  <!--https://cn.vuejs.org/guide/essentials/conditional.html#v-if-vs-v-show-->

  <!--列表渲染-->
  <!--基本使用-->
  <li v-for="item in items">
    {{ item.message }}
  </li>
  <el-divider />
  <!--第二个参数表示当前项的位置索引-->
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
  <!--解构-->
  <el-divider />
  <li v-for="{ message } in items">
    {{ message }}
  </li>
  <el-divider />
  <!-- 有 index 索引时 -->
  <li v-for="({ message }, index) in items">{{ message }} {{ index }}</li>
  <el-divider />

  <!--v-for和对象-->
  <ul>
    <li v-for="value in myObject">
      {{ value }}
    </li>
  </ul>
  <!--可以通过提供第二个参数表示属性名 (例如 key)-->
  <ul>
    <li v-for="(value, key) in myObject">{{ key }} : {{ value }}</li>
  </ul>
  <!--第三个参数表示索引-->
  <ul>
    <li v-for="(value, key, index) in myObject">
      {{ index }}. {{ key }}: {{ value }}
    </li>
  </ul>

  <!--组件中使用v-for:https://cn.vuejs.org/guide/essentials/list.html#v-for-with-a-component-->
</template>

<!--
v-if可以加到template上
<template v-if="flag">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>-->
