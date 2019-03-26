<template>
  <div class="todo-add-item">
    <form id="add-form" @submit.prevent="add">
      <input v-model="item" type="text" placeholder="Add Item" class="todo-input" name="todo">
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
      item: ''
    }
  },
  methods: {
    add() {
      if (this.item !== '') this.$emit('add', this.item)
      this.item = ''
    }
  }
}
</script>

