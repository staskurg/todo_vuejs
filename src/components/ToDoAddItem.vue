<template>
  <div class="todo-add-item">
    <form id="add-form" @submit.prevent="addTodo">
      <input v-model="newTodo" type="text" placeholder="Add Item" class="todo-input" name="todo">
      <button type="submit" class="btn btn-add-todo">
        <i class="fas fa-plus"></i> Add
      </button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: ''
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo !== '') this.$emit('add', this.newTodo)
      this.newTodo = ''
    }
  }
}
</script>

