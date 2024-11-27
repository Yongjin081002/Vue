<template>
    <div>
      <button @click="toggleVisibility">토글</button>
      <p v-if="isVisible">안녕하세요!</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        isVisible: true
      };
    },
    methods: {
      toggleVisibility() {
        this.isVisible = !this.isVisible;
      }
    }
  };
  </script>
  