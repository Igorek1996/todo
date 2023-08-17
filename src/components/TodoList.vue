<template>
  <div class="todo-list">
    <ul class="todo-list__list">
      <li class="todo-item" v-for="todo in todos" :key="todo.id" :todo="todo">
        <label class="todo-item__label" :class="{ completed: todo.completed }">
          <span class="checkbox-container">
            <input
              class="checkbox"
              type="checkbox"
              :checked="todo.completed"
              @change="editCompleted(todo)"
            />
            <span class="checkmark"></span>
          </span>

          <span class="todo-item__text">{{ todo.title }}</span>
        </label>
        <div class="todo-item__buttons">
          <button class="btn" @click="openModal(todo.id)">Редактировать</button>
          <button class="btn" @click="deleteTodo(todo.id)">Удалить</button>
        </div>
      </li>
    </ul>
    <div class="todo-list__footer">
      <p>
        Выполненных задач: <strong>{{ checkedLength }}</strong>
      </p>
      <p>
        Осталось задач: <b>{{ uncheckedLength }}</b>
      </p>
      <p>
        Всего задач: <b>{{ todosLength }}</b>
      </p>
    </div>

    <TodoModal v-if="isEditing" @closeModal="closeEditModal">
      <form class="form todo-modal__form" @submit.prevent="editTodo">
        <h2>Редактировать задачу</h2>
        <input class="form__field" type="text" v-model="changedTitle" />
        <button class="btn" type="submit">Сохранить</button>
      </form>
    </TodoModal>
  </div>
</template>

<script setup>
import TodoModal from "./TodoModal.vue";
import { defineProps, ref, defineEmits, computed } from "vue";

const props = defineProps({
  todos: Array,
});

const isEditing = ref(false);
const changedTitle = ref("");
const changedId = ref(0);
const changedComleted = ref(false);

const emit = defineEmits();

const openModal = (id) => {
  const todoEdit = props.todos.find((todo) => todo.id === id);

  if (todoEdit) {
    changedId.value = todoEdit.id;
    changedTitle.value = todoEdit.title;
    changedComleted.value = todoEdit.completed;
    isEditing.value = true;
  }
};

const closeEditModal = () => {
  isEditing.value = false;
  changedId.value = null;
  changedTitle.value = "";
  changedComleted.value = false;
};

const editTodo = () => {
  emit("editTodo", {
    id: changedId.value,
    title: changedTitle.value,
    completed: changedComleted.value,
  });
  closeEditModal();
};

const editCompleted = (todo) => {
  emit("editTodo", {
    id: todo.id,
    title: todo.title,
    completed: !todo.completed,
  });
};

const deleteTodo = (id) => {
  emit("deleteTodo", id);
};

const checkedLength = computed(() => {
  return props.todos.filter((todo) => todo.completed).length;
});
const uncheckedLength = computed(() => {
  return props.todos.filter((todo) => !todo.completed).length;
});
const todosLength = computed(() => {
  return props.todos.length;
});
</script>

<style lang="scss" scoped>
.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  padding: 10px;
  border-bottom: 1px solid #ccc;

  &__label {
    cursor: pointer;
    position: relative;
    display: flex;
    flex: 0 1 100%;
    overflow: hidden;
    gap: 10px;
    &.completed {
      text-decoration: line-through;
      color: #888;
    }
  }
  &__text {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    font-size: 16px;
  }

  &__buttons {
    display: flex;
    gap: 10px;
  }
}
</style>
