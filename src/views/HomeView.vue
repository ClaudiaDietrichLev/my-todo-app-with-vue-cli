<template>
  <div class="home">
    <LayoutHeader />
    <AddTodo />
    <div class="todosSection">
      <div class="filters">
        <MainButton
          @click="deleteDoneTodos()"
          buttonTitle="Delete done todos"
          buttonStyle="button-delete"
        />
      </div>
      <ListTodos :todos="todos" />
    </div>
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
    };
  },
  created() {
    this.getAllTodos();
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
    },
  },
};
</script>

<style scoped>
.filters {
  display: flex;
  justify-content: center;
  margin-block: 1em;
  align-items: center;
}

@media screen and (min-width: 768px) {
  .todosSection {
    display: grid;
    gap: 40px;
    grid-template-columns: auto 1fr;
  }
}
</style>
