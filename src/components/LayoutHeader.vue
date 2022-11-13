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
  padding-block: 10px;
}
h1 {
  color: var(--color-bg);
  margin: 0;
  text-align: center;
}
</style>
