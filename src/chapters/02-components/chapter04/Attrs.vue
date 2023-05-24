<!--透传Attributes-->
<script setup lang="ts">
import MyButton from '@/chapters/02-components/chapter04/MyButton.vue';

function onClick() {
  console.log('clicked');
}
</script>

<template>
  <!--
  1.Attributes 继承
  “透传 attribute”指的是传递给一个组件，却没有被该组件声明为 props 或 emits 的 attribute
  或者 v-on 事件监听器。最常见的例子就是 class、style 和 id。
  当一个组件以单个元素为根作渲染时，透传的 attribute 会自动被添加到根元素上
  下面这个例子渲染出来的DOM是
  <button class="large">click me</button>
  这里，<MyButton> 并没有将 class 声明为一个它所接受的 prop，
  所以 class 被视作透传 attribute，自动透传到了 <MyButton> 的根元素上
  -->
  <MyButton class="large" id="no1" @click="onClick" />
  <!--
  1.1. 对 class 和 style 的合并
  如果一个子组件的根元素已经有了 class 或 style attribute，它会和从父组件上继承的值合并。
  如果我们将之前的 <MyButton> 组件的模板改成这样
  button class="btn">click me</button>
  那么渲染出来的DOM是
  <button class="btn large">click me</button>
  -->

  <!--
  1.2. v-on 监听器继承
  同样的规则也适用于 v-on 事件监听器
  <MyButton @click="onClick" />
  click 监听器会被添加到 <MyButton> 的根元素，即那个原生的 <button> 元素之上。
  当原生的 <button> 被点击，会触发父组件的 onClick 方法。同样的，
  如果原生 button 元素自身也通过 v-on 绑定了一个事件监听器，则这个监听器和从父组件继承的监听器都会被触发
  -->

  <!--
  1.3. 深层组件继承
  有些情况下一个组件会在根节点上渲染另一个组件。
  例如，我们重构一下 <MyButton>，让它在根节点上渲染 <BaseButton>：
  <MyButton/> 的模板，只是渲染另一个组件：
  <BaseButton />
  此时 <MyButton> 接收的透传 attribute 会直接继续传给 <BaseButton>
  A -> B -> C 这样
  -->

  <!--
  2.禁用 Attributes 继承 和 $attrs
  最常见的需要禁用 attribute 继承的场景就是 attribute 需要应用在根节点以外的其他元素上。
  通过设置 inheritAttrs 选项为 false，你可以完全控制透传进来的 attribute 被如何使用。
  这些透传进来的 attribute 可以在模板的表达式中直接用 $attrs 访问到。
  https://cn.vuejs.org/guide/components/attrs.html#disabling-attribute-inheritance
  -->

  <!--
  3. 多根节点的 Attributes 继承 
  4. 在 JavaScript 中访问透传 Attributes
  查看MyButton组件内容~~
  -->
</template>

<style scoped></style>
