<template>
  <div class="todo-list">
    <h1>Todo App</h1>
    <h3 v-if="hasItems">{{ listTitle }}</h3>
    <TodoAddItem @add="add($event)"/>
    <div class="todo-items">
      <TodoItem
        v-for="(item, i) in list"
        :key="item.id"
        :title="item.title"
        :completed="item.completed"
        @save="save(item, $event)"
        @complete="complete(item)"
        @delete="deleteItem(i)"
      />
    </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue'
import TodoAddItem from './TodoAddItem.vue'

export default {
  name: 'TodoList',
  components: {
    TodoItem,
    TodoAddItem
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
    items() {
      return this.list.length
    },
    hasItems() {
      return this.items > 0
    },
    listTitle() {
      return `Currently ${this.items} todo ${this.items === 1 ? 'item' : 'items'} in the list`
    }
  },
  watch: {
    items(newVal, OldVal) {
      console.log(`Watching for todoItems. New Items length ${newVal} and Old Items length ${OldVal}`)
    }
  },
  created() {
    console.log('This item was created')
  },
  methods: {
    add(val) {
      this.list.push({
        title: val,
        completed: false,
        id: this.getRandom(1000, 100000000000000).toString()
      })
    },
    deleteItem(i) {
      this.list.splice(i, 1)
    },
    complete(item) {
      item.completed = !item.completed
    },
    save(item, val) {
      item.title = val
    },
    getRandom(min, max) {
      min = Math.ceil(min)
      max = Math.floor(max)
      return Math.floor(Math.random() * (max - min + 1)) + min
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
