<template>
  <div>
    <h1>{{ title }}</h1>
    <div class="todo-container">
      <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add task">

      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          <span :class="[{'is-completed': todo.completed}, 'text']">{{ todo.text }}</span>
          <input type="checkbox" v-model="todo.completed">
          <button @click="removeTodo">Erase</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
  import { ref } from 'vue'

  defineProps({
    title: String
  })

  // Define the array of to-dos
  const todos = ref([])

  // Define the new to-do input
  const newTodo = ref('')

  // Function to add a new to-do
  const addTodo = () => {
    todos.value.push({
      text: newTodo.value,
      completed: false
    })
    newTodo.value = ''
  }

  // Function to remove a to-do
  const removeTodo = (index) => {
    todos.value.splice(index, 1)
  }
</script>

<style scoped>
  .is-completed {
    text-decoration: line-through;
  }
</style>
