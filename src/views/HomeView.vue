<template>
  <div class="home">
    <LayoutHeader />
    <AddTodo />
    <DeleteDoneTodos :todos="this.todos" />

    <ListTodos :todos="this.todos" />
  </div>
</template>

<script>
// @ is an alias to /src
import LayoutHeader from "@/components/LayoutHeader.vue";
import ListTodos from "@/components/ListTodos.vue";
import DeleteDoneTodos from "@/components/DeleteTodo.vue";
import AddTodo from "@/components/AddTodo.vue";

export default {
  name: "HomeView",
  components: { LayoutHeader, ListTodos, AddTodo, DeleteDoneTodos },
  data() {
    return {
      todos: [],
    };
  },
  async created() {
    const response = await fetch("http://localhost:4730/todos");
    this.todos = await response.json();
  },
};
</script>
