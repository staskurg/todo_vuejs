<template>
  <div :class="{'item_is-completed' : todo.completed }" class="item">
    <div v-show="!isEditing" class="item__show">
      <div class="btn_complete" @click="$emit('complete')">
        <h3>{{ todo.title }}</h3>
      </div>
      <div class="btn__group">
        <button v-if="!todo.completed" class="btn btn_edit" @click="toggleForm">
          <i class="fas fa-edit"></i>
        </button>
        <button class="btn btn_delete" @click="$emit('delete')">
          <i class="fas fa-trash-alt"></i>
        </button>
      </div>
    </div>
    <div v-show="isEditing" class="item__edit">
      <form id="edit-form" @submit.prevent="editTodo">
        <div class="edit-input">
          <input
            :value="todoNewValue = todo.title"
            type="text"
            class="todo-input"
            @input="todoNewValue = $event.target.value"
          >
        </div>
        <div class="btn__group">
          <button class="btn btn_save" type="submit">
            <i class="fas fa-check"></i>
          </button>
          <button class="btn btn_cancel" @click="toggleForm">
            <i class="fas fa-times"></i>
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ToDo',
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      isEditing: false,
      todoNewValue: ''
    }
  },
  methods: {
    editTodo() {
      this.$emit('save', this.todoNewValue)
      this.isEditing = false
    },
    toggleForm() {
      this.isEditing = !this.isEditing
    }
  }
}
</script>

<style>
.item {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  background: #ffffff;
  border-radius: 5px;
  margin-bottom: 10px;
  width: 100%;
  height: 60px;
  text-align: left;
  background-color: rgba(0, 0, 0, 0.05);
  border: 1px solid rgba(0, 0, 0, 0.1);
  box-sizing: border-box;
  position: relative;
}
.item:hover {
  background-color: rgba(0, 0, 0, 0.1);
  border-color: rgba(0, 0, 0, 0.15);
}
.item_is-completed {
  text-decoration: line-through;
  background-color: rgba(0, 128, 0, 0.15);
  border-color: rgba(0, 128, 0, 0.2);
}
.item_is-completed:hover {
  background-color: rgba(0, 128, 0, 0.25);
  border-color: rgba(0, 128, 0, 0.3);
}
.item__show {
  width: 100%;
  height: 100%;
  cursor: pointer;
}
.btn__group {
  position: absolute;
  right: 15px;
  top: 15px;
  bottom: 0;
}
.btn__group > :not(:last-child) {
  margin-right: 5px;
}
.btn {
  cursor: pointer;
  width: 30px;
  height: 30px;
}
.btn_complete {
  width: 100%;
  height: 100%;
  padding: 0 15px;
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.btn_delete,
.btn_cancel {
  background-color: #ec5840;
  color: #fefefe;
  border: none;
  border-radius: 4px;
}
.btn_delete:hover,
.btn_cancel:hover {
  background-color: #da3116;
}
.btn_edit {
  background-color: #ffae00;
  color: #fefefe;
  border: none;
  border-radius: 4px;
}
.btn_edit:hover {
  background-color: #cc8b00;
}
.btn_save {
  background-color: #28a745;
  color: #fefefe;
  border: none;
  border-radius: 4px;
}
.btn_save:hover {
  background-color: #218838;
}
.edit-input {
  padding-left: 15px;
}
</style>


