<script setup lang="ts">
import { Todo } from '@/types'
import AppTodoItem from './AppTodoItem.vue'

const props = defineProps<{ todos: Todo[] }>()

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
  <ul class="todo-list">
    <AppTodoItem
      v-for="todo in todos"
      :todo="todo"
      :key="todo.id"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />
  </ul>
</template>

<style scoped></style>
