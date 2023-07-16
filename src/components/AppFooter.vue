<script setup lang="ts">
import { Stats } from '@/types'
const props = defineProps<{ stats: Stats }>()
</script>

<template>
  <footer class="app-footer">
    {{ `${stats.active} more to do, ${stats.done} done` }}
  </footer>
</template>

<style scoped></style>
