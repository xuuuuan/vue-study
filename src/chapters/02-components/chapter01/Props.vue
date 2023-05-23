<!--Props-->
<script setup lang="ts">
// 1.Props 声明
// 一个组件需要显式声明它所接受的 props，
// 这样 Vue 才能知道外部传入的哪些是 props，
// 哪些是透传 attribute (关于透传 attribute，会在第四章节中讨论)。
// defineProps<{
//   title?: string;
//   likes?: number;
// }>();

// 2.传递 prop 的细节 查看官网即可~
// https://cn.vuejs.org/guide/components/props.html#prop-passing-details

// 3.单向数据流
// 所有的 props 都遵循着单向绑定原则，props 因父组件的更新而变化，
// 自然地将新的状态向下流往子组件，而不会逆向传递。
// https://cn.vuejs.org/guide/components/props.html#one-way-data-flow

// 4.Prop 校验
// 5.Boolean 类型转换
// 都查看官网即可
</script>

<template>
  <div>哈哈</div>
</template>

<style scoped></style>
