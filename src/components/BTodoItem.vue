<script setup lang="ts">
import {TodoItem} from "@/types/TodoItem";

defineProps<{ todoItem: TodoItem }>()

defineEmits(['delete', 'done'])
</script>

<template>
  <li class="list-group-item d-flex justify-content-between align-items-center border-start-0 border-top-0 border-end-0 border-bottom rounded-0 mb-2">
    <div class="d-flex align-items-center">
      <input class="form-check-input me-2" type="checkbox" :value="todoItem.done" @click="$emit('done', todoItem)"/>
      <span :class="todoItem.done ? 'text-decoration-line-through' : null">{{ todoItem.title }}</span>
    </div>
    <a @click="$emit('delete', todoItem)" data-mdb-toggle="tooltip" title="Remove item">
      <i class="fa fa-times text-primary"></i>
    </a>
  </li>
</template>

<style scoped>

</style>
