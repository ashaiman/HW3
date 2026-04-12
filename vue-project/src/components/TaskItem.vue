<script setup>
defineProps({
  task: {
    type: Object,
    required: true,
  },
})

const emit = defineEmits(['toggle-task', 'delete-task'])
</script>

<template>
  <li class="task-item">
    <div>
      <input
        type="checkbox"
        :checked="task.completed"
        @change="emit('toggle-task', task.id)"
      />

      <span :class="{ completed: task.completed }">
        {{ task.title }}
      </span>
    </div>

    <p>
      Priority: {{ task.priority }} | Category: {{ task.category }}
    </p>

    <button type="button" @click="emit('delete-task', task.id)">
      Delete
    </button>
  </li>
</template>

<style scoped>
.task-item {
  border: 1px solid #ddd;
  padding: 1rem;
  margin-bottom: 0.75rem;
  list-style: none;
}

.completed {
  text-decoration: line-through;
  color: gray;
}

button {
  cursor: pointer;
}
</style>
