<script setup>
import { ref } from 'vue'
import TaskForm from '../components/TaskForm.vue'

const tasks = ref([])

function addTask(task) {
  tasks.value.push(task)
}
</script>

<template>
  <section>
    <h1>Task Dashboard</h1>
    <p>This is where my task manager will go.</p>

    <TaskForm @add-task="addTask" />

    <h2>Tasks</h2>

    <ul>
      <li v-for="task in tasks" :key="task.title">
        {{ task.title }} - {{ task.priority }} - {{ task.category }}
      </li>
    </ul>
  </section>
</template>

<style scoped>
section {
  padding: 2rem;
}

h1 {
  color: #1f2937;
}
</style>
