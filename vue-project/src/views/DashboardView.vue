<script setup>
import { computed, ref, watch } from 'vue'
import TaskForm from '../components/TaskForm.vue'
import TaskItem from '../components/TaskItem.vue'
import TaskStats from '../components/TaskStats.vue'

const savedTasks = localStorage.getItem('tasks')
const tasks = ref(savedTasks ? JSON.parse(savedTasks) : [])
const statusFilter = ref('All')
const searchTerm = ref('')

const completedTasks = computed(() => tasks.value.filter((task) => task.completed))
const activeTasks = computed(() => tasks.value.filter((task) => !task.completed))

const filteredTasks = computed(() => {
  const search = searchTerm.value.toLowerCase()

  return tasks.value.filter((task) => {
    const matchesStatus =
      statusFilter.value === 'All' ||
      (statusFilter.value === 'Active' && !task.completed) ||
      (statusFilter.value === 'Completed' && task.completed)

    const matchesSearch =
      task.title.toLowerCase().includes(search) ||
      task.priority.toLowerCase().includes(search) ||
      task.category.toLowerCase().includes(search)

    return matchesStatus && matchesSearch
  })
})

watch(
  tasks,
  () => {
    localStorage.setItem('tasks', JSON.stringify(tasks.value))
  },
  { deep: true },
)

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

    <TaskStats
      :total="tasks.length"
      :active="activeTasks.length"
      :completed="completedTasks.length"
    />

    <TaskForm @add-task="addTask" />

    <div class="controls">
      <label>
        Search Tasks
        <input v-model="searchTerm" type="search" placeholder="Search by title, priority, category" />
      </label>

      <div class="filters">
        <button
          v-for="filter in ['All', 'Active', 'Completed']"
          :key="filter"
          type="button"
          :class="{ selected: statusFilter === filter }"
          @click="statusFilter = filter"
        >
          {{ filter }}
        </button>
      </div>
    </div>

    <h2>Tasks</h2>

    <ul v-if="filteredTasks.length">
      <TaskItem
        v-for="task in filteredTasks"
        :key="task.id"
        :task="task"
        @toggle-task="toggleTask"
        @delete-task="deleteTask"
      />
    </ul>

    <p v-else class="empty">No tasks found.</p>
  </section>
</template>

<style scoped>
section {
  max-width: 850px;
  margin: 0 auto;
  padding: 2rem;
}

ul {
  padding: 0;
}

h1 {
  color: #3b236a;
}

.controls {
  display: grid;
  gap: 1rem;
  margin-top: 1.5rem;
}

label {
  display: grid;
  gap: 0.35rem;
  font-weight: bold;
}

input {
  background: #ffffff;
  border: 1px solid #c9b3ea;
  border-radius: 8px;
  padding: 0.7rem;
  font: inherit;
}

.filters {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

button {
  background: #ffffff;
  border: 1px solid #c9b3ea;
  border-radius: 8px;
  color: #4c1d95;
  cursor: pointer;
  padding: 0.6rem 0.9rem;
}

button.selected {
  background: #5b21b6;
  border-color: #5b21b6;
  color: white;
}

.empty {
  color: #666;
  font-style: italic;
}
</style>
