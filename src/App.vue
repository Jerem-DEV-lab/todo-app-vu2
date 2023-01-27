<template>
  <div class="container">
    <div class="logo">
      <img src="./assets/check-logo.png" alt="logo" />
    </div>
    <h2 class="app__title">Todo App by <span>Guillemet Jeremy</span>.</h2>
    <todo-list />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
export default {
  name: 'App',
  components: {
    TodoList,
  },
}
</script>

<style src="./styles/app.scss" lang="scss"></style>