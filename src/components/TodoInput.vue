<template>
  <div class="inputBox">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <button v-on:click="addTodo">add</button>
    <Modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">
        경고!
        <button class="closeModalBtn" @click="showModal = false">
          X
        </button>
      </h3>
      <h5 slot="body">내용을 입력하세요.</h5>
    </Modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue';
export default {
  data() {
    return {
      newTodoItem: '',
      showModal: false,
    };
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== '') {
        this.$emit('addTodoItem', this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = '';
    },
  },
  components: {
    Modal,
  },
};
</script>

<style scoped>
input:focus {
  outline: none;
}

.closeModalBtn {
  color: red;
}
</style>
