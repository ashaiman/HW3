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
  background: #ffffff;
  border: 1px solid #c9b3ea;
  border-radius: 8px;
  box-shadow: 0 4px 14px rgba(92, 55, 145, 0.08);
  padding: 1rem;
  margin-bottom: 0.75rem;
  list-style: none;
}

.completed {
  text-decoration: line-through;
  color: #8b76ad;
}

button {
  background: #7c3aed;
  border: 0;
  border-radius: 8px;
  color: white;
  cursor: pointer;
  padding: 0.5rem 0.8rem;
}
</style>
