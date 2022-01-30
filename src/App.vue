<template>
  <div id="app">
    <ToDoApp></ToDoApp>
  </div>
</template>

<script>
import ToDoApp from "./components/TodoApp.vue";

export default {
  name: "App",
  components: {
    ToDoApp,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  background-color: paleturquoise;
  height: 100vh;
}
</style>
