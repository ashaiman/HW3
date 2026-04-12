<script setup>
import { ref } from 'vue'
import TaskForm from '../components/TaskForm.vue'
import TaskItem from '../components/TaskItem.vue'

const tasks = ref([])

function addTask(task) {
  const newTask = {
    id: Date.now(),
    title: task.title,
    priority: task.priority,
    category: task.category,
    completed: false,
  }
  tasks.value.push(newTask)
}

function toggleTask(id) {
  const task = tasks.value.find((task) => task.id === id)
  if (task) {
    task.completed = !task.completed
  }
}

function deleteTask(id) {
  tasks.value = tasks.value.filter((task) => task.id !== id)
}
</script>

<template>
  <section>
    <h1>Task Dashboard</h1>
    <p>This is where my task manager will go.</p>

    <TaskForm @add-task="addTask" />

    <h2>Tasks</h2>

    <ul>
      <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @toggle-task="toggleTask"
        @delete-task="deleteTask"
      />
    </ul>
  </section>
</template>

<style scoped>
section {
  padding: 2rem;
}

ul {
  padding: 0;
}

h1 {
  color: #1f2937;
}
</style>
