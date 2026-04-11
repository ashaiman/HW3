<script setup></script>

<template>
  <header>
    <h1>TaskFlow</h1>

    <nav>
      <RouterLink to="/">Dashboard</RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </nav>
  </header>

  <main>
    <RouterView />
  </main>
</template>

<style scoped>
header {
  padding: 1rem 2rem;
  border-bottom: 1px solid #ddd;
}

nav {
  display: flex;
  gap: 1rem;
}

a {
  color: #2563eb;
  font-weight: bold;
}

main {
  padding: 1rem;
}
</style>
