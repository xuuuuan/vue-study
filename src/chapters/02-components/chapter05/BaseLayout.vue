<script setup lang="ts"></script>

<template>
  <div class="container">
    <!--<slot> 元素可以有一个特殊的 attribute name，
    用来给各个插槽分配唯一的 ID，以确定每一处要渲染的内容-->
    <header>
      <slot name="header"></slot>
    </header>
    <!--这类带 name 的插槽被称为具名插槽 (named slots)。
    没有提供 name 的 <slot> 出口会隐式地命名为“default”-->
    <main>
      <slot />
    </main>
    <footer>
      <slot name="footer"></slot>
    </footer>
  </div>
</template>

<style scoped>
footer {
  border-top: 1px solid #ccc;
  color: #666;
  font-size: 0.8em;
}
</style>
