<template>
  <div class="todo-list">
    <h1>Todo App</h1>
    <h3 v-if="hasItems">{{ listTitle }}</h3>
    <ToDoAddItem @add="addTodo($event)"/>
    <div class="todo-items">
      <ToDoItem
        v-for="(todoItem, index) in list"
        :key="todoItem.id"
        :todo="todoItem"
        @delete="deleteTodo(index)"
        @complete="completeTodo(todoItem)"
        @save="saveTodo(todoItem, $event)"
      />
    </div>
  </div>
</template>

<script>
import ToDoItem from './ToDoItem.vue'
import ToDoAddItem from './ToDoAddItem.vue'

export default {
  name: 'TodoList',
  components: {
    ToDoItem,
    ToDoAddItem
  },
  data() {
    return {
      list: [
        {
          title: 'Clean the house',
          completed: true,
          id: '123678345'
        },
        {
          title: 'Walk the dog',
          completed: false,
          id: '678234567'
        },
        {
          title: 'Wash the car',
          completed: false,
          id: '789345678'
        },
        {
          title: 'Do laundry',
          completed: false,
          id: '6783478'
        }
      ]
    }
  },
  computed: {
    todoItems() {
      return this.list.length
    },
    hasItems() {
      return this.todoItems > 0
    },
    listTitle() {
      return `Currently ${this.todoItems} todo ${this.todoItems === 1 ? 'item' : 'items'} in the list`
    }
  },
  watch: {
    todoItems(newVal, OldVal) {
      console.log(`Watching for todoItems. New Items length ${newVal} and Old Items length ${OldVal}`)
    }
  },
  created() {
    console.log('This item was created')
  },
  methods: {
    addTodo(value) {
      this.list.push({
        title: value,
        completed: false
      })
    },
    deleteTodo(index) {
      this.list.splice(index, 1)
    },
    completeTodo(item) {
      item.completed = !item.completed
    },
    saveTodo(item, value) {
      item.title = value
    }
  }
}
</script>

<style>
.todo-list {
  max-width: 500px;
  min-width: 300px;
  margin: auto;
  padding: 15px;
  background-color: #ffffff;
  border-radius: 10px;
  box-shadow: 0px 0.25rem 1rem rgba(0, 0, 0, 0.25);
}
.todo-add-item {
  width: 100%;
  line-height: 24px;
  margin-bottom: 20px;
  position: relative;
}
.todo-input {
  width: 100%;
  height: 30px;
  box-sizing: border-box;
  padding: 5px;
  border-radius: 4px;
  border: 1px solid #cacaca;
  padding: 0 70px 0 15px;
}
.btn-add-todo {
  width: 60px;
  background-color: #2199e8;
  color: #fefefe;
  border: none;
  border-top-right-radius: 4px;
  border-bottom-right-radius: 4px;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  padding: 0 10px;
}
.btn-add-todo:hover {
  background-color: #1583cc;
}
</style>
