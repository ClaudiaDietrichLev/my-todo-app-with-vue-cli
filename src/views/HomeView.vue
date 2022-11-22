<template>
  <div class="home">
    <LayoutHeader />
    <AddTodo />
    <div class="container">
      <MainButton
        @click="deleteDoneTodos()"
        buttonTitle="Delete done todos"
        buttonStyle="button-delete"
      />
    </div>

    <ListTodos :todos="this.todos" />
  </div>
</template>

<script>
// @ is an alias to /src
import LayoutHeader from "@/components/LayoutHeader.vue";
import ListTodos from "@/components/ListTodos.vue";
import MainButton from "@/components/MainButton.vue";
import AddTodo from "@/components/AddTodo.vue";

export default {
  name: "HomeView",
  components: { LayoutHeader, ListTodos, AddTodo, MainButton },
  data() {
    return {
      todos: [],
      changedTodos: false,
    };
  },
  created() {
    this.getAllTodos();
  },
  watch: {
    changedTodos(oldValue) {
      if (oldValue) {
        this.getAllTodos();
      }
    },
  },
  methods: {
    deleteDoneTodos() {
      const doneTodos = this.todos.filter((todo) => todo.done === true);
      for (let doneTodo of doneTodos) {
        this.deleteTodo(doneTodo);
      }
      if (doneTodos.length > 0) {
        this.changedTodos = true;
      }
      return this.changedTodos;
    },
    async deleteTodo(todo) {
      const response = await fetch("http://localhost:4730/todos/" + todo.id, {
        method: "delete",
      });
      return response;
    },

    async getAllTodos() {
      const response = await fetch("http://localhost:4730/todos");
      this.todos = await response.json();
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  margin-block: 1em;
}
</style>
