<template>
  <div>
    <ul>
      <li
        v-for="(todoItem, index) in todoItems"
        v-bind:key="todoItem.item"
        v-bind:class="{ textCompleted: todoItem.completed }"
      >
        <button v-on:click="toggleTodo(todoItem, index)">체크</button>
        {{ todoItem.item }}
        <button v-on:click="removeTodo(todoItem)">삭제</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoItems: [],
      checked: false,
    };
  },
  created() {
    console.log(this.todoItems);
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server')
          this.todoItems.push(
            JSON.parse(localStorage.getItem(localStorage.key(i))),
          );
      }
    }
  },
  methods: {
    removeTodo(todoItem, index) {
      console.log(todoItem);
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
    toggleTodo(todoItem) {
      console.log(todoItem);
      todoItem.completed = !todoItem.completed;
      // 로컬스토리지의 데이터를 갱신(completed의 변화)
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
  },
};
</script>

<style>
ul,
li {
  list-style: none;
  padding: 0;
}

.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
</style>
