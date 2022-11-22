<template>
  <form>
    <label for="add-todo" class="visually-hidden">Add a new todo</label>
    <input
      id="add-todo"
      class="input-todo-description"
      type="text"
      v-model="textTodo"
      placeholder="add a new Todo"
    />
    <MainButton
      @click="addNewTodo()"
      buttonTitle="Add"
      buttonStyle="button-add"
    />
  </form>
</template>

<script>
import MainButton from "@/components/MainButton.vue";

export default {
  name: "AddTodo",
  data() {
    return {
      textTodo: "",
      stateTodo: false,
      newTodo: {},
    };
  },
  components: {
    MainButton,
  },
  methods: {
    async addNewTodo() {
      (this.newTodo.description = this.textTodo),
        (this.newTodo.done = this.stateTodo);
      const response = await fetch("http://localhost:4730/todos", {
        method: "post",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(this.newTodo),
      });
      return response;
    },
  },
};
</script>

<style scoped>
input {
  all: unset;
  background-color: var(--color-bg-input);
  border-radius: 5px;
  padding: 0.5em;
  width: 100%;
  border: 2px solid transparent;
}

form {
  padding-top: 1em;
  display: flex;
  gap: 1em;
  margin: auto;
  justify-content: center;
  margin-inline: 3em;
}

input::placeholder {
  color: var(--color-accent-pink);
}

input:focus {
  border: 2px solid var(--color-accent-yellow);
}
</style>
