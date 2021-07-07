<template>
  <li class="d-flex align-items-center list-none list-group-item">
    <input
      type="checkbox"
      class="todoCheckbox"
      @click="$emit('on-toggle')"
      v-if="!isEditing"
    />
    <button @click="$emit('on-toggle')" v-if="!isEditing">
      <span>{{ description }}</span>
    </button>
    <form v-else class="flex-grow-1" @submit.prevent="finishEditing()">
      <input
        type="text"
        class="form-control"
        v-model="newTodoDescription"
        @blur="finishEditing()"
        ref="newTodo"
      />
    </form>
    <button @click="startEditing()">
      <span>Edit</span>
    </button>
    <button @click="$emit('on-delete')" class="btn btn-outline-danger border-0">
      <span>DEL</span>
    </button>
  </li>
</template>

<script>
export default {
  data() {
    return {
      isEditing: false,
      newTodoDescription: ""
    };
  },
  props: {
    description: String,
    completed: Boolean
  },
  methods: {
    startEditing() {
      if (this.isEditing) {
        this.finishEditing();
      } else {
        this.newTodoDescription = this.description;
        this.isEditing = true;
        this.$nextTick(() => this.$refs.newTodo.focus());
      }
    },
    finishEditing() {
      this.isEditing = false;
      this.$emit("on-edit", this.newTodoDescription);
    }
  }
};
</script>
