<template>
  <div class="todo-item">
    <div
      :class="{'todo-completed' : todo.completed }"
      class="btn-complete"
      @click="$emit('complete')"
    >
      <h3>{{ todo.title }}</h3>
    </div>
    <button class="btn btn-delete" @click="$emit('delete')">
      <i class="fas fa-times"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  props: {
    todo: {
      type: Object,
      required: true
    }
  }
}
</script>

<style>
.todo-item {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  background: #ffffff;
  border-radius: 5px;
  margin-bottom: 10px;
  cursor: pointer;
  width: 100%;
  height: 60px;
  text-align: left;
  background-color: rgba(0, 0, 0, 0.05);
  border: 1px solid rgba(0, 0, 0, 0.1);
  box-sizing: border-box;
  position: relative;
}
.todo-item:hover {
  background-color: rgba(0, 0, 0, 0.1);
  border-color: rgba(0, 0, 0, 0.15);
}
.todo-completed {
  text-decoration: line-through;
  background-color: rgba(0, 128, 0, 0.15);
  border-color: rgba(0, 128, 0, 0.2);
}
.todo-completed:hover {
  background-color: rgba(0, 128, 0, 0.25);
  border-color: rgba(0, 128, 0, 0.3);
}
.btn {
  cursor: pointer;
}
.btn-complete {
  width: 100%;
  padding: 0 15px;
}
.btn-delete {
  background-color: #ec5840;
  color: #fefefe;
  border: none;
  width: 30px;
  height: 30px;
  position: absolute;
  right: 15px;
  top: 15px;
  bottom: 0;
  border-radius: 4px;
}
.btn-delete:hover {
  background-color: #da3116;
}
</style>


