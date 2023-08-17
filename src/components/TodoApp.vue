<template>
  <main class="todo-app">
    <TodoForm @addTodo="addTodo" />
    <TodoList :todos="todos" @deleteTodo="deleteTodo" @editTodo="editTodo" />
  </main>
</template>

<script setup>
import TodoList from "./TodoList.vue";
import TodoForm from "./TodoForm.vue";
import { ref, onMounted, watch } from "vue";

const todos = ref([]);

const addTodo = (title) => {
  todos.value.push({
    id: Date.now(),
    title: title,
    completed: false,
  });
};

const editTodo = (editingTodo) => {
  const index = todos.value.findIndex((todo) => todo.id === editingTodo.id);
  todos.value.splice(index, 1, editingTodo);
};

const deleteTodo = (id) => {
  const index = todos.value.findIndex((todo) => todo.id === id);
  if (index !== -1) {
    todos.value.splice(index, 1);
  }
};

onMounted(() => {
  if (
    JSON.parse(localStorage.getItem("todos")) &&
    JSON.parse(localStorage.getItem("todos")).length
  )
    todos.value = JSON.parse(localStorage.getItem("todos"));
});

watch(
  todos,
  (newTodos) => {
    localStorage.setItem("todos", JSON.stringify(newTodos));
  },
  { deep: true }
);
</script>

<style lang="scss" scoped>
.todo-app {
  border-left: 2px solid;
  border-right: 2px solid;
  flex: 1 1 100%;
}
</style>
