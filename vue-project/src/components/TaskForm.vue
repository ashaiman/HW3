<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add-task'])

const title = ref('')
const priority = ref('Medium')
const category = ref('')

function submitTask() {
  if (title.value.trim() === '' || category.value.trim() === '') {
    return
  }

  const newTask = {
    title: title.value,
    priority: priority.value,
    category: category.value,
  }

  emit('add-task', newTask)

  title.value = ''
  priority.value = 'Medium'
  category.value = ''
}
</script>

<template>
  <form @submit.prevent="submitTask">
    <h2>Add a Task</h2>

    <label>
      Task Title
      <input v-model="title" type="text" placeholder="Enter a task" />
    </label>

    <label>
      Priority
      <select v-model="priority">
        <option>High</option>
        <option>Medium</option>
        <option>Low</option>
      </select>
    </label>

    <label>
      Category
      <input v-model="category" type="text" placeholder="School, Work, Personal" />
    </label>

    <button type="submit">Add Task</button>
  </form>
</template>

<style scoped>
form {
  background: #ffffff;
  border: 1px solid #c9b3ea;
  border-radius: 8px;
  box-shadow: 0 4px 14px rgba(92, 55, 145, 0.1);
  display: grid;
  gap: 1rem;
  max-width: 400px;
  padding: 1rem;
}

label {
  display: grid;
  gap: 0.3rem;
  font-weight: bold;
}

input,
select,
button {
  border: 1px solid #c9b3ea;
  border-radius: 8px;
  padding: 0.7rem;
  font: inherit;
}

button {
  background: #5b21b6;
  color: white;
  cursor: pointer;
}
</style>
