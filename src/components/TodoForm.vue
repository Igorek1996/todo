<template>
  <form class="form todo-form" @submit.prevent="addTodo">
    <input
      class="todo-form__field form__field"
      v-model="newTodo"
      placeholder="Введите новую задачу"
    />
    <button class="btn todo-form__btn" type="submit">Добавить</button>
  </form>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const emit = defineEmits();
const newTodo = ref("");

const addTodo = () => {
  if (newTodo.value && newTodo.value.trim().length) {
    emit("addTodo", newTodo.value);
    newTodo.value = "";
  }
};
</script>

<style lang="scss" scoped>
.todo-form {
  width: 100%;
  display: flex;
  justify-content: space-between;
  gap: 10px;
  padding: 10px;

  &__field {
    flex: 0 1 100%;
  }
}
</style>
