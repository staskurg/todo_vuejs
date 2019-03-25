<template>
  <div class="todo-list">
    <h1>Todo App</h1>
    <h3
      v-if="todoItems > 0"
    >Currently {{ todoItems }} todo {{todoItems === 1 ? 'item' : 'items'}} in the list</h3>
    <div class="todo-add-item">
      <input
        v-model="newTodo"
        type="text"
        placeholder="Add Item"
        class="todo-input"
        @keyup.enter="addTodo"
      >
      <button class="btn btn-add-todo" @click="addTodo">
        <i class="fas fa-plus"></i> Add
      </button>
    </div>
    <div class="todo-items">
      <todo
        v-for="(todoItem, index) in todoData"
        :key="todoItem.title + index"
        :todo="todoItem"
        @delete="deleteTodo(index)"
        @complete="completeTodo(todoItem)"
      />
    </div>
  </div>
</template>

<script>
import Todo from './components/Todo.vue'

export default {
  name: 'TodoList',
  components: {
    Todo
  },
  data() {
    return {
      todoData: [
        {
          title: 'Clean the house',
          completed: true
        },
        {
          title: 'Walk the dog',
          completed: false
        },
        {
          title: 'Wash the car',
          completed: false
        },
        {
          title: 'Do laundry',
          completed: false
        }
      ],
      newTodo: ''
    }
  },
  computed: {
    todoItems() {
      return this.todoData.length
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
    addTodo() {
      if (this.newTodo) {
        this.todoData.push({
          title: this.newTodo,
          completed: false
        })
        this.newTodo = ''
      }
    },
    deleteTodo(index) {
      this.todoData.splice(index, 1)
    },
    completeTodo(item) {
      item.completed = !item.completed
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
  height: 30px;
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

