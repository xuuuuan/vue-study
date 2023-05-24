<script setup lang="ts">
import { ref } from 'vue';
import FancyButton from '@/chapters/02-components/chapter05/FancyButton.vue';
import BaseLayout from '@/chapters/02-components/chapter05/BaseLayout.vue';
import DefaultScopeSlot from '@/chapters/02-components/chapter05/DefaultScopeSlot.vue';
import NamedScopeSlot from '@/chapters/02-components/chapter05/NamedScopeSlot.vue';
import FancyList from '@/chapters/02-components/chapter05/FancyList.vue';

const message = ref('click me');
</script>

<template>
  <span>{{ message }}</span>
  <FancyButton>
    <span>please </span>
    <!--
    1. 渲染作用域
    插槽内容可以访问到父组件的数据作用域，因为插槽内容本身是在父组件模板中定义的
    父组件模板中的表达式只能访问父组件的作用域；子组件模板中的表达式只能访问子组件的作用域。
    -->
    {{ message }}
  </FancyButton>
  <!--2. 默认内容-->
  <FancyButton />
  <el-divider />
  <!--3. 具名插槽-->
  <BaseLayout>
    <template v-slot:header>
      <h1>Here might be a page title</h1>
    </template>
    <!--    
    <template #default>
    <p>A paragraph for the main content.</p>
    <p>And another one.</p>
    </template>
    -->
    <!-- 
    当一个组件同时接收默认插槽和具名插槽时，
    所有位于顶级的非 <template> 节点都被隐式地视为默认插槽的内容
    隐式的默认插槽:
    -->
    <p>A paragraph for the main content.</p>
    <p>And another one.</p>
    <!--v-slot: 简写# -->
    <template #footer>
      <p>Here's some contact info</p>
    </template>
  </BaseLayout>
  <el-divider />

  <!--
  4. 作用域插槽
  在上面的渲染作用域中我们讨论到，插槽的内容无法访问到子组件的状态。
  然而在某些场景下插槽的内容可能想要同时使用父组件域内和子组件域内的数据。
  要做到这一点，我们需要一种方法来让子组件在渲染时将一部分数据提供给插槽。
  -->

  <!--
  4.1. 默认作用域插槽
  当需要接收插槽 props 时，默认插槽和具名插槽的使用方式有一些小区别。
  默认插槽接受 props，通过子组件标签上的 v-slot 指令，直接接收到了一个插槽 props 对象
  可以理解为访问对象里的属性
  -->
  <DefaultScopeSlot v-slot="slotProps">
    {{ slotProps.text }} {{ slotProps.count }}
  </DefaultScopeSlot>
  <el-divider />

  <!--4.2. 具名作用域插槽 跟默认作用域插槽差不多-->
  <NamedScopeSlot>
    <template #header="props">
      {{ props.message }}
    </template>
    <!--对象的解构-->
    <template #default="{ message }">
      {{ message }}
    </template>
    <template #footer="footerProps">
      {{ footerProps }}
    </template>
  </NamedScopeSlot>
  <el-divider />

  <!--4.3. 
  高级列表组件示例
  你可能想问什么样的场景才适合用到作用域插槽，这里我们来看一个 <FancyList> 组件的例子。
  它会渲染一个列表，并同时会封装一些加载远端数据的逻辑、使用数据进行列表渲染、或者是像分页或无限滚动这样更进阶的功能。
  然而我们希望它能够保留足够的灵活性，将对单个列表元素内容和样式的控制权留给使用它的父组件。
  -->
  <FancyList per-page="url" api-url="10">
    <template #item="{ body, username, likes }">
      <p>{{ body }}</p>
      <p class="meta">by {{ username }} | {{ likes }} likes</p>
    </template>
  </FancyList>
</template>

<style scoped>
.meta {
  font-size: 0.8em;
  color: #42b883;
}
</style>
