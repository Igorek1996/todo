<template>
  <div class="app">
    <TodoHeader />
    <TodoApp />
    <TodoFooter />
  </div>
</template>

<script setup>
import TodoHeader from "./components/TodoHeader.vue";
import TodoFooter from "./components/TodoFooter.vue";
import TodoApp from "./components/TodoApp.vue";
</script>

<style scoped>
.app {
  width: 600px;
  max-width: 100%;
  min-height: 100vh;

  margin: 0 auto;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
</style>
