<!--
<script>
// 使用普通的 <script> 来声明选项
export default {
  // 禁用 Attributes 继承
  inheritAttrs: false
}
</script>
-->

<script setup lang="ts">
import { useAttrs } from 'vue';
// 4. 在 JavaScript 中访问透传 Attributes
const attrs = useAttrs();
console.log(attrs);
</script>

<template>
  <span>Fallthrough attribute: {{ $attrs }}</span>
  <!--3. 多根节点的 Attributes 继承 需要 $attrs 被显式绑定-->
  <button v-bind="$attrs">click me</button>
</template>

<style scoped></style>
