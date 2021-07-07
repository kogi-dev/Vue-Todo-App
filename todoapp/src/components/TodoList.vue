<template>
  <div class="container grid col-3">
    <div class="row">
      <div class="">
        <h1>{{ listName }}</h1>
      </div>
    </div>
    <div class="row">
      <create-todo @on-new-todo="addTodo($event)" />
    </div>
    <div class="row">
      <ul class="list-none">
        <todo
          index="0"
          v-for="(todo, index) in todos"
          :key="KeyGenerator(index)"
          :description="todo.description"
          :completed="todo.completed"
          @on-toggle="toggleTodo(todo)"
          @on-delete="deleteTodo(todo)"
          @on-edit="editTodo(todo, $event)"
        />
      </ul>
    </div>
    <div class="row">
      <button @onclick="checkAll()" class="h-12 text-lg rounded-lg">
        Alle Boxen abhaken
      </button>
    </div>
  </div>
</template>

<script>
import Todo from "./Todo.vue";
import CreateTodo from "./CreateTodo.vue";

export default {
  name: "TodoList",
  props: {
    listName: String
  },
  data() {
    return {
      todos: [
        { description: "Rasenmähen bei Oma", completed: false },
        { description: "Einkaufen gehen", completed: false },
        { description: "Sammeln von Himbeeren", completed: false }
      ]
    };
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push({ description: newTodo, completed: false });
    },
    toggleTodo(todo) {
      todo.completed = !todo.completed;
      var inputs = document.querySelectorAll("todoCheckbox");
      inputs[todo.key].checked = todo.completed;
    },
    deleteTodo(deletedTodo) {
      this.todos = this.todos.filter(todo => todo !== deletedTodo);
    },
    editTodo(todo, newTodoDescription) {
      todo.description = newTodoDescription;
    },
    checkAll(TodoList) {
      var inputs = document.querySelectorAll(".todoCheckbox");
      for (var i = 0; i < inputs.length; i++) {
        inputs[i].checked = true;
        TodoList[i].completed = true;
      }
    }
  },

  components: { Todo, CreateTodo }
};
</script>
