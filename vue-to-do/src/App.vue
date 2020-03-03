<template>
  <div>
    <add-To-Do></add-To-Do>
  </div>
</template>

<script>
import AddToDo from "./components/Add-todo.vue";

export default {
  components: {
    "add-To-Do": AddToDo
  },
  name: "app",
  data() {
    return {};
  }
};
</script>

<style lang="scss">
</style>
