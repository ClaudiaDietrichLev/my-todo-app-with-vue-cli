<template>
  <div class="todo-list">
    <ul>
      <h2>Your Todos</h2>
      <li v-for="todo in todos" :key="todo">
        <input
          type="checkbox"
          class="checkboxTodo"
          v-model="todo.done"
          :id="'todo-done-' + todo.id"
          @change="updateTodo(todo)"
        />
        <label :for="'todo-done-' + todo.id">{{ todo.description }}</label>
      </li>
    </ul>
    {{ todos }}
  </div>
</template>

<script>
export default {
  name: "ListTodos",
  props: {
    todos: [],
  },
  methods: {
    async updateTodo(todo) {
      const response = await fetch("http://localhost:4730/todos/" + todo.id, {
        method: "put",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(todo),
      });
      todo = await response.json();
    },
  },
};
</script>

<style scoped>
ul {
  display: flex;
  flex-direction: column;
  margin: auto;
}
li {
  list-style: none;
  background-color: var(--color-bg-input);
  border-radius: 5px;

  padding-block: 0.5em;
  padding-inline: 0.5em;
  margin-right: 3em;
  margin-bottom: 1em;
}

.checkboxTodo:checked {
  color: var(--color-bg-input);
  accent-color: var(--color-accent-green);
  outline: 1px solid var(--color-accent-yellow);
  _background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' aria-hidden='true' focusable='false' %3E%3Cpath fill='none' stroke='white' stroke-width='3' d='M1.73 12.91l6.37 6.37L22.79 4.59' /%3E%3C/svg%3E");
}

.checkboxTodo + label {
  padding-left: 0.5em;
}

.visually-hidden {
  border: 0;
  clip: rect(0 0 0 0);
  height: auto;
  margin: 0;
  overflow: hidden;
  padding: 0;
  position: absolute;
  width: 1px;
  white-space: nowrap;
}
</style>
