<template>
  <div class="home">
    <LayoutHeader />
    <form>
      <label for="add-todo" class="visually-hidden">Add a new todo</label>
      <input
        id="add-todo"
        class="input-todo-description"
        type="text"
        v-model="textTodo"
        placeholder="add a new Todo"
        ref="description"
      />
      <MainButton
        @click.prevent="addNewTodo()"
        buttonTitle="Add"
        buttonStyle="button-add"
      />
    </form>

    <div class="todo-section">
      <div class="filters">
        <div class="filter-container">
          <div class="radio-button">
            <input
              type="radio"
              v-model="filter"
              name="filter"
              id="filter-all"
              value="all"
            />
            <label for="filter-all">All</label>
          </div>
          <div class="radio-button">
            <input
              type="radio"
              v-model="filter"
              name="filter"
              id="filter-open"
              value="open"
            />
            <label for="filter-open">Open</label>
          </div>
          <div class="radio-button">
            <input
              type="radio"
              v-model="filter"
              name="filter"
              id="filter-done"
              value="done"
            />
            <label for="filter-done">Done</label>
          </div>
        </div>
        <MainButton
          @click="deleteDoneTodos()"
          buttonTitle="Delete done todos"
          buttonStyle="button-delete"
        />
      </div>
      <ListTodos :todos="todosToList" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import LayoutHeader from "@/components/LayoutHeader.vue";
import ListTodos from "@/components/ListTodos.vue";
import MainButton from "@/components/MainButton.vue";

export default {
  name: "HomeView",
  components: { LayoutHeader, ListTodos, MainButton },
  data() {
    return {
      todos: [],
      textTodo: "",
      stateTodo: false,
      newTodo: {},
      filter: "all",
      todosToList: [],
    };
  },
  created() {
    this.getAllTodos();
  },
  watch: {
    filter() {
      if (this.filter === "open") {
        this.todosToList = this.todos.filter((todo) => todo.done === false);
      } else if (this.filter === "done") {
        this.todosToList = this.todos.filter((todo) => todo.done === true);
      } else {
        this.todosToList = this.todos.filter(
          (todo) => todo.done === false || todo.done === true
        );
      }
    },
  },

  methods: {
    deleteDoneTodos() {
      const doneTodos = this.todos.filter((todo) => todo.done === true);
      const deleteRequests = doneTodos.map(this.deleteTodo);
      Promise.all(deleteRequests).then(() => {
        this.getAllTodos();
      });
    },
    async deleteTodo(todo) {
      return fetch("http://localhost:4730/todos/" + todo.id, {
        method: "delete",
      });
    },

    async getAllTodos() {
      const response = await fetch("http://localhost:4730/todos");
      this.todos = await response.json();
      this.todosToList = [];

      // bessere Lösung?
      for (let todo of this.todos) {
        this.todosToList.push(todo);
      }
    },
    addNewTodo() {
      this.newTodo.description = this.textTodo;
      this.newTodo.done = this.stateTodo;
      this.addNewTodoToApi(this.newTodo);
      this.textTodo = "";
      this.$refs.description.focus();
    },
    async addNewTodoToApi(todo) {
      const response = await fetch("http://localhost:4730/todos", {
        method: "post",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(todo),
      }).then(this.getAllTodos());
      return response;
    },
  },
};
</script>

<style scoped>
.input-todo-description {
  all: unset;
  background-color: var(--color-bg-input);
  border-radius: 5px;
  padding: 0.5em;
  width: 100%;
  border: 2px solid transparent;
}
.radio-button {
  display: flex;
  gap: 0.5em;
}

form {
  padding-top: 1em;
  display: flex;
  gap: 1em;
  margin: auto;
  justify-content: center;
  margin-inline: 3em;
}

.input-todo-description::placeholder {
  color: var(--color-accent-pink);
}

.input-todo-description:focus {
  border: 2px solid var(--color-accent-yellow);
}

.filters {
  display: flex;
  flex-direction: column;
  justify-content: start;
  margin-block: 1em;
  align-items: center;
  margin-inline: 3em;
}

.filter-container {
  background-color: var(--color-bg-input);
  margin: 1em;
  padding: 0.5em;
  display: flex;
  justify-content: space-between;
  width: 100%;
  border-radius: 5px;
  border: 2px solid var(--color-accent-blue);
}
@media screen and (min-width: 768px) {
  .todo-section {
    display: grid;
    gap: 40px;
    grid-template-columns: auto 1fr;
  }
  .filter-container {
    flex-direction: column;
    justify-content: start;
  }
}
</style>
