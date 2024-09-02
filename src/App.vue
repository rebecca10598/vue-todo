<template>
  <div id="app">
    <TodoList /> <!-- Use imported and registered component here -->
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'; // Import the component

export default {
  name: 'App',
  components: {
    TodoList // Register the component
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
