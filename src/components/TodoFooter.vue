<template>
  <div>
    <button v-on:click="clearAll">모두 삭제</button>
  </div>
</template>

<script>
export default {
  methods: {
    clearAll() {
      localStorage.clear();
    },
  },
};
</script>

<style></style>
