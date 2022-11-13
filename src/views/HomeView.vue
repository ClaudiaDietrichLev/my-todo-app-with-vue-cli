<template>
  <div class="home">
    <LayoutHeader />
  </div>
</template>

<script>
// @ is an alias to /src
import LayoutHeader from "@/components/LayoutHeader.vue";

export default {
  name: "HomeView",
  components: {
    LayoutHeader,
  },
};
</script>
