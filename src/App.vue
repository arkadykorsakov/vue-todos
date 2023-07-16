<script setup lang="ts">
import AppHeader from './components/AppHeader.vue'
import AppFilters from './components/AppFilters.vue'
import AppTodoList from './components/AppTodoList.vue'
import AppAddTodo from './components/AppAddTodo.vue'
import AppFooter from './components/AppFooter.vue'

import { ComputedRef, Ref, computed, ref } from 'vue'
import { Filter, Stats, Todo } from '@/types'

const todos: Ref<Todo[]> = ref([{ id: 1, text: 'kkk', completed: true }])
const activeFilter: Ref<Filter> = ref('All')

const activeTodos: ComputedRef<Todo[]> = computed(() =>
  todos.value.filter((todo) => !todo.completed)
)

const doneTodos: ComputedRef<Todo[]> = computed(() =>
  todos.value.filter((todo) => todo.completed)
)

const filteredTodos: ComputedRef<Todo[]> = computed<Todo[]>(() => {
  switch (activeFilter.value) {
    case 'Active':
      return activeTodos.value
    case 'Done':
      return doneTodos.value
    case 'All':
    default:
      return todos.value
  }
})

const stats: ComputedRef<Stats> = computed<Stats>(() => {
  return { active: activeTodos.value.length, done: doneTodos.value.length }
})

const toggleTodo = (id: number): void => {
  todos.value = todos.value.map((todo) =>
    todo.id === id ? { ...todo, completed: !todo.completed } : todo
  ) as Todo[]
}

const removeTodo = (id: number): void => {
  todos.value = todos.value.filter((todo) => {
    todo.id !== id
  }) as Todo[]
}

const addTodo = (newTodo: Todo): void => {
  todos.value.push(newTodo)
}

const setFilter = (filter: Filter) => {
  activeFilter.value = filter
}
</script>
<template>
  <AppHeader />
  <AppFilters :active-filter="activeFilter" @set-filter="setFilter" />
  <main class="app-main">
    <AppTodoList
      :todos="filteredTodos"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />
    <AppAddTodo @add-todo="addTodo" />
  </main>
  <AppFooter :stats="stats" />
</template>

<style>
@import url('@/assets/app.css');
</style>
