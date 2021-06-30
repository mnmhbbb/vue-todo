<template>
  <div>
    <transition-group name="test" tag="ul">
      <li
        v-for="(todoItem, index) in propsdata"
        v-bind:key="todoItem.item"
        v-bind:class="{ textCompleted: todoItem.completed }"
      >
        <button v-on:click="toggleTodo(todoItem, index)">체크</button>
        {{ todoItem.item }}
        <button v-on:click="removeTodo(todoItem, index)">삭제</button>
      </li>
    </transition-group>
  </div>
</template>

<script>
export default {
  props: ['propsdata'],
  methods: {
    removeTodo(todoItem, index) {
      this.$emit('removeTodoItem', todoItem, index);
    },
    toggleTodo(todoItem, index) {
      this.$emit('toggleTodoItem', todoItem, index);
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

.test-enter-active,
.test-leave-active {
  transition: all 1s;
}
.test-enter,
.test-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
</style>
