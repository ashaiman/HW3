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
:global(body) {
  margin: 0;
  background: #f1e8ff;
  color: #2f2545;
  font-family: 'Courier New', Courier, monospace;
}

header {
  background: #ffffff;
  box-shadow: 0 4px 14px rgba(92, 55, 145, 0.12);
  padding: 1rem 2rem;
  border-bottom: 1px solid #d8c4f2;
}

nav {
  display: flex;
  gap: 1rem;
}

a {
  color: #6d28d9;
  font-weight: bold;
}

main {
  padding: 1rem;
}

@media (max-width: 650px) {
  header {
    padding: 1rem;
  }

  nav {
    flex-direction: column;
  }
}
</style>
