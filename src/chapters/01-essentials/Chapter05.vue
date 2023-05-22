<!--表单输入绑定-->
<script setup lang="ts">
import { ref } from 'vue';

const message = ref('');
const checked = ref(false);
const picked = ref('lb');
const selected = ref('');
const modifier = ref('');
</script>

<template>
  <!--1.基本用法-->
  <!--1.1.文本-->
  <p>Message is: {{ message }}</p>
  <el-input v-model="message" style="width: 200px" placeholder="edit me" />
  <el-divider />
  <!--1.2.多行文本-->
  <span>Multiline message is:</span>
  <p style="white-space: pre-line">{{ message }}</p>
  <el-input
    v-model="message"
    type="textarea"
    rows="5"
    placeholder="add multiple lines"
  />
  <el-divider />
  <!--1.3.复选框-->
  <el-checkbox v-model="checked" label="Checkbox">{{ checked }}</el-checkbox>
  <el-divider />
  <!--1.4.单选按钮-->
  <p>Picked: {{ picked }}</p>
  <el-radio v-model="picked" label="lb">李白</el-radio>
  <el-radio v-model="picked" label="hx">韩信</el-radio>
  <el-radio v-model="picked" label="zy">赵云</el-radio>
  <el-divider />
  <!--1.5.选择列表-->
  <div>Selected: {{ selected }}</div>
  <el-select v-model="selected" placeholder="请选择">
    <el-option label="李白" value="lb"></el-option>
    <el-option label="韩信" value="hx"></el-option>
    <el-option label="赵云" value="zy"></el-option>
  </el-select>
  <el-divider />

  <!--2.值绑定-->
  <!--上面案例中的复选框、单选按钮中的label 选择列表中的value就是值绑定-->
  <!--html的原生标签的值绑定会不一样 但是大同小异-->

  <!--3.修饰符-->
  <!--3.1. .lazy-->
  <!--在默认情况下，v-model 在 input 事件中同步输入框的值与数据 (除了 上述 ime 事件)。
  你可以添加 lazy 修饰符，从而转变为在 change 事件中同步-->
  <div>{{ modifier}}</div>
  <el-input v-model.lazy="modifier" style="width: 200px" placeholder="edit me" />
  <el-divider />
  <!--3.2. .number-->
  <!--如果想自动将用户的输入值转为数值类型，可以给 v-model 添加 number 修饰符-->
  <el-input v-model.number="modifier" style="width: 200px" placeholder="edit me" />
  <el-divider />
  <!--3.3. .trim-->
  <!--如果要自动过滤用户输入的首尾空白字符，可以给 v-model 添加 trim 修饰符-->
  <el-input v-model.trim="modifier" style="width: 200px" placeholder="edit me" />
</template>

<style scoped></style>
