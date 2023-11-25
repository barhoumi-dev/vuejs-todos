<script setup lang="ts">
import BTodoItem from "./BTodoItem.vue";
import type {TodoItem} from "@/types/TodoItem";
import BTodoItemForm from "./BTodoItemForm.vue";
import {computed, ref} from "vue";
import {useLocalStorage} from "@vueuse/core";


const todos: TodoItem[] = useLocalStorage('demo-todo-items', [])

const countTotal = computed(() => todos.value.length)
const countDone = computed(() => todos.value.filter((item) => item.done).length)

function onSaveItem(todoItem: TodoItem) {
  todoItem.createAt = new Date()
  todoItem.id = todoItem.createAt.toString()

  todos.value.push(todoItem)
}

function onDeleteItem(todoItem: TodoItem) {
  todos.value = todos.value.filter((todo) => todo.id !== todoItem.id)
}

function onDoneItem(todoItem: TodoItem) {
  todoItem.done = !todoItem.done
  todoItem.doneAt = todoItem.done ? new Date() : null
}
</script>

<template>
  <div class="card" style="border-radius: 15px;">
    <div class="card-body p-5">
      <h6 class="mb-3">Awesome Todo List</h6>

      <BTodoItemForm @submit="onSaveItem"/>

      <ul class="list-group mb-0">
        <BTodoItem
            v-for="todo in todos"
            :todo-item="todo"
            :key="todo.createAt"
            @done="onDoneItem"
            @delete="onDeleteItem"
        />
      </ul>
    </div>
    <div class="card-footer">
      <span>{{ countDone }} dones</span> /
      <span>{{ countTotal }} totals</span>
    </div>
  </div>
</template>

<style>

</style>
