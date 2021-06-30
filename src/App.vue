<template>
  <div id="app">
    <todo-header></todo-header>
    <todo-input v-on:addTodoItem="addItem"></todo-input>
    <todo-list
      v-bind:propsdata="todoItems"
      v-on:removeTodoItem="removeItem"
      v-on:toggleTodoItem="toggleTodo"
    ></todo-list>
    <todo-footer v-on:clearAll="clearAllTodo"></todo-footer>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {
  data() {
    return {
      todoItems: [],
    };
  },
  methods: {
    addItem(todoItem) {
      const obj = { completed: false, item: todoItem };
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj); // 화면과 동기화
    },
    removeItem(todoItem, index) {
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
    toggleTodo(todoItem, index) {
      this.todoItems[index].completed = !this.todoItems[index].completed;
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllTodo() {
      localStorage.clear();
      this.todoItems = [];
    },
  },
  created() {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server')
          this.todoItems.push(
            JSON.parse(localStorage.getItem(localStorage.key(i))),
          );
      }
    }
  },
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter,
  },
};
</script>

<style>
body {
  text-align: center;
  background-color: #e5e5e5;
}
input {
  border-style: groove;
}
</style>
