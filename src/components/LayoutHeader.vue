<template>
  <header>
    <h1>Todo App</h1>
    <p>Get your things done</p>
  </header>
</template>

<script>
export default { name: "LayoutHeader" };
</script>

<style scoped>
header {
  background-color: var(--color-accent-pink);
  padding-block: 1rem;
  text-align: center;
}
h1 {
  color: var(--color-bg);
  margin: 0;
  padding-top: 1rem;
  font-size: 3em;
  letter-spacing: 0.1em;
  text-shadow: 1px 3px var(--color-accent-yellow),
    3px 5px var(--color-accent-blue);
}

p {
  font-size: 1.25em;
  color: var(--color-bg);
}
</style>
