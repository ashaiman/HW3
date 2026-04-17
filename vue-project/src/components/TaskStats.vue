<script setup>
defineProps({
  total: {
    type: Number,
    required: true,
  },
  active: {
    type: Number,
    required: true,
  },
  completed: {
    type: Number,
    required: true,
  },
})
</script>

<template>
  <section class="stats">
    <article>
      <span>Total</span>
      <strong>{{ total }}</strong>
    </article>

    <article>
      <span>Active</span>
      <strong>{{ active }}</strong>
    </article>

    <article>
      <span>Completed</span>
      <strong>{{ completed }}</strong>
    </article>
  </section>
</template>

<style scoped>
.stats {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(3, 1fr);
  margin: 1.5rem 0;
}

article {
  background: #ffffff;
  border: 1px solid #c9b3ea;
  border-radius: 8px;
  box-shadow: 0 4px 14px rgba(92, 55, 145, 0.08);
  padding: 1rem;
}

span {
  color: #6b5a85;
  display: block;
  font-size: 0.9rem;
}

strong {
  color: #3b236a;
  font-size: 1.7rem;
}

@media (max-width: 650px) {
  .stats {
    grid-template-columns: 1fr;
  }
}
</style>
