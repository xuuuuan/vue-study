<script setup lang="ts">
import CustomInput from '@/chapters/02-components/chapter03/CustomInput.vue';
import Arguments from '@/chapters/02-components/chapter03/Arguments.vue';
import UserName from '@/chapters/02-components/chapter03/UserName.vue';
import Modifier from '@/chapters/02-components/chapter03/Modifier.vue';
import { ref } from 'vue';

const message = ref('hello world');

const firstName = ref('Seven');
const lastName = ref('Zhou');

const text = ref('');
</script>

<template>
  <h1>{{ message }}</h1>
  <!--1.v-model 基本使用-->
  <CustomInput v-model="message" />
  <!--2.v-model 的参数-->
  <Arguments v-model:msg="message" />
  <el-divider />
  <!--3.多个 v-model 绑定-->
  <h1>{{ firstName }} {{ lastName }}</h1>
  <UserName v-model:first-name="firstName" v-model:last-name="lastName" />
  <el-divider />
  <!--4.处理v-model 修饰符-->
  <Modifier v-model:text.upper="text" />
</template>

<style scoped></style>
