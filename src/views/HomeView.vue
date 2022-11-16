<template>
  <div class="home">
    <LayoutHeader />
    <ListTodos />
  </div>
</template>

<script>
// @ is an alias to /src
import LayoutHeader from "@/components/LayoutHeader.vue";
import ListTodos from "@/components/ListTodos.vue";

export default {
  name: "HomeView",
  components: {
    LayoutHeader,
    ListTodos,
  },
};
</script>
