<script setup lang="ts">
import { Todo } from '@/types'
import { Ref, reactive, ref } from 'vue'

interface State {
  text: string
}

const emit = defineEmits<{
  (e: 'addTodo', textTodo: Todo): void
}>()

const isFormVisible: Ref<boolean> = ref(false)
const state: State = reactive({
  id: 0,
  completed: false,
  text: ''
})

const showForm = (): void => {
  isFormVisible.value = true
}

const hideForm = (): void => {
  isFormVisible.value = false
}

const addTodo = () => {
  const newTodo: Todo = {
    id: Date.now(),
    text: state.text,
    completed: false
  }
  emit('addTodo', newTodo)
  state.text = ''
}
</script>

<template>
  <section class="add-todo">
    <form v-if="isFormVisible" class="add-todo__form" @submit.prevent="addTodo">
      <button class="close-button" type="button">
        <i class="bi bi-x" @click="hideForm"></i>
      </button>
      <div class="text-input text-input--focus">
        <input class="input" v-model.trim="state.text" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button v-else class="add-todo__show-form-button" @click="showForm">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<style scoped></style>
