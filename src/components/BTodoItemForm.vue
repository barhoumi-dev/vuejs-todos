<script setup>
import {ref} from "vue";

const emit = defineEmits(['submit'])

const title = ref('')

function saveTodo() {
  if (title.value.trim() !== '') {
    emit('submit', {title: title.value})
    title.value = ''
  }
}
</script>

<template>
  <form class="d-flex justify-content-center align-items-center mb-4">
    <div class="form-outline flex-fill">
      <input v-model="title" type="text" placeholder="What do you need to do today?" id="form3"
             class="form-control form-control-lg"/>
    </div>
    <button type="submit" class="btn btn-primary btn-lg ms-2" @click.prevent="saveTodo">Add</button>
  </form>
</template>

<style scoped lang="scss">
</style>
