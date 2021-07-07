<template>
  <todo-list list-name="Macherjek Todo-List" />
</template>

<script>
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",
  components: {
    TodoList
  }
};
</script>
