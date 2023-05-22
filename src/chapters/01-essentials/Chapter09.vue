<!--组件基础-->
<script setup lang="ts">
import { ref } from 'vue';
import ChildButtonCounter from '@/chapters/01-essentials/ChildButtonCounter.vue';
import ChildBlogPost from '@/chapters/01-essentials/ChildBlogPost.vue';
import ChildFancyButton from '@/chapters/01-essentials/ChildFancyButton.vue';

const posts = ref([
  { id: 1, title: 'My journey with Vue', content: 'content 1' },
  { id: 2, title: 'Blogging with Vue', content: 'content 2' },
  { id: 3, title: 'Why Vue is so fun', content: 'content 3' },
]);

const postFontSize = ref(1);
</script>

<template>
  <!--1.使用组件-->
  <h1>Here are many child components!</h1>
  <ChildButtonCounter />
  <ChildButtonCounter />
  <ChildButtonCounter />
  <el-divider />
  <!--2.传递 props、3.监听事件-->
  <div :style="{ fontSize: `${postFontSize}em` }">
    <ChildBlogPost
      v-for="post in posts"
      :key="post.id"
      :title="post.title"
      :content="post.content"
      @enlarge-text="postFontSize += 0.1"
      @reduce-text="postFontSize -= 0.1"
    />
  </div>
  <el-divider />
  <!--3.通过插槽来分配内容-->
  <ChildFancyButton>
    <!-- slot content -->
    Click me
  </ChildFancyButton>
  <!--4.动态组件-->
  <!-- 
  有些场景会需要在两个组件间来回切换，比如 Tab 界面：
  currentTab 改变时组件也改变 
  <component :is="tabs[currentTab]"></component>
  在上面的例子中，被传给 :is 的值可以是以下几种：
  1.被注册的组件名
  2.导入的组件对象
  你也可以使用 is attribute 来创建一般的 HTML 元素。
  当使用 <component :is="..."> 来在多个组件间作切换时，被切换掉的组件会被卸载。
  我们可以通过 <KeepAlive> 组件强制被切换掉的组件仍然保持“存活”的状态。
  -->
</template>

<style scoped></style>
