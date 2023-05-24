<script setup lang="ts"></script>

<template>
  <div class="container">
    <header>
      <slot name="header" message="Header"></slot>
    </header>
    <main>
      <slot message="Main" />
    </main>
    <footer>
      <slot name="footer" message="Footer"></slot>
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
