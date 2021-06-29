<template>
  <div class="inputBox">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <button v-on:click="addTodo">add</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodoItem: '',
    };
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== '') {
        const obj = { completed: false, item: this.newTodoItem };
        localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
        this.clearInput();
      }
    },
    clearInput() {
      this.newTodoItem = '';
    },
  },
};
</script>

<style scoped>
input:focus {
  outline: none;
}
</style>
