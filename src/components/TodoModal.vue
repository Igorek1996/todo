<template>
  <div class="todo-modal">
    <div class="todo-modal__content">
      <slot></slot>
      <button class="btn" @click="closeModal">Закрыть</button>
    </div>
  </div>
</template>

<script setup>
import { defineEmits } from "vue";

const emit = defineEmits();

const closeModal = () => {
  emit("closeModal");
};
</script>

<style lang="scss">
.todo-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;

  &__content {
    display: flex;
    flex-direction: column;
    gap: 10px;
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);

    button {
      margin-top: 10px;
    }
  }

  &__form {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
}
</style>
