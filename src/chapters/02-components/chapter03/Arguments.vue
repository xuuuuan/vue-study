<script setup lang="ts">
// 默认情况下，v-model 在组件上都是使用 modelValue 作为 prop，
// 并以 update:modelValue 作为对应的事件。
// 我们可以通过给 v-model 指定一个参数来更改这些名字：
// 这里我们定义的是msg  所以使用的时候需要 v-model:msg="..."
defineProps<{
  msg: string;
}>();
defineEmits<{
  (event: 'update:msg', value: string): void;
}>();
</script>

<template>
  <div>
    <input :value="msg" @input="$emit('update:msg', $event.target.value)" />
    <p>{{ msg }}</p>
  </div>
</template>

<style scoped></style>
