<template>
  <MainButton
    @click="deleteDoneTodos()"
    buttonTitle="Delete done todos"
    buttonStyle="button-delete"
  />
</template>

<script>
import MainButton from "@/components/MainButton.vue";

export default {
  name: "DeleteTodo",
  props: {
    todos: [],
  },

  components: {
    MainButton,
  },
  methods: {
    deleteDoneTodos() {
      const doneTodos = this.todos.filter((todo) => todo.done === true);
      for (let doneTodo of doneTodos) {
        this.deleteTodo(doneTodo);
      }
    },
    async deleteTodo(todo) {
      const response = await fetch("http://localhost:4730/todos/" + todo.id, {
        method: "delete",
      });
      return response;
    },
  },
};
</script>
