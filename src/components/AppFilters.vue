<script setup lang="ts">
import { Filter } from '@/types'
const props = defineProps<{ activeFilter: Filter }>()
const emit = defineEmits<{
  (e: 'setFilter', filter: Filter): void
}>()

const filters: Filter[] = ['Active', 'All', 'Done']

const setFilter = (filter: Filter): void => {
  emit('setFilter', filter)
}
</script>

<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
        v-for="filter in filters"
        :key="filter"
        :class="['button', { 'button--primary': activeFilter === filter }]"
        @click="setFilter(filter)"
      >
        {{ filter }}
      </button>
    </section>
  </aside>
</template>

<style scoped></style>
