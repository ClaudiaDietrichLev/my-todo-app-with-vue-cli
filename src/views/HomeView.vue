<template>
  <div class="home">
    <LayoutHeader />
    <AddTodo></AddTodo>

    <ListTodos />
  </div>
</template>

<script>
// @ is an alias to /src
import LayoutHeader from "@/components/LayoutHeader.vue";
import ListTodos from "@/components/ListTodos.vue";

import AddTodo from "@/components/AddTodo.vue";

export default {
  name: "HomeView",
  components: { LayoutHeader, ListTodos, AddTodo },
};
</script>
