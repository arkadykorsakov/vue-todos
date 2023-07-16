<script setup lang="ts">
import { Todo } from '@/types'

const props = defineProps<{
  todo: Todo
}>()

const emit = defineEmits<{
  (e: 'toggleTodo', id: number): void
  (e: 'removeTodo', id: number): void
}>()

const toggleTodo = (id: number): void => {
  emit('toggleTodo', id)
}

const removeTodo = (id: number): void => {
  emit('removeTodo', id)
}
</script>

<template>
  <li
    :class="['todo-item', { 'todo-item--done': todo.completed }]"
    @click="toggleTodo(todo.id)"
  >
    <div class="todo-item__status">
      <i class="bi bi-check2"></i>
    </div>
    <span class="todo-item__text"> {{ todo.text }}</span>
    <button class="todo-item__remove-button" @click.stop="removeTodo(todo.id)">
      <i class="bi bi-trash3"></i>
    </button>
  </li>
</template>

<style scoped></style>
