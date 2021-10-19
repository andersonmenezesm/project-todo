<template>
  <body>
    <todo-list />
  </body>
</template>

<script>
import TodoList from './components/TodoList.vue'
export default {
  components: { TodoList },
  name: 'App'
}
</script>

<style>
body {
  background-color: #212529;
  font-family: 'Montserrat', 'Avenir', 'Helvetica', 'Arial', sans-serif;
  font-size: 16px;
}
#app {
  padding: 3rem;
  display: grid;
  grid-template-columns: minmax(0px, 400px);
  grid-gap: 2rem;
}
</style>
