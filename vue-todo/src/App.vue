<template>
  <main id="app">
    <TodoHeader msg="Vue Todo List!"/>
    <TodoList/>
  </main>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoList from './components/TodoList.vue';

export default {
  name: 'app',
  components: {
    TodoHeader,
    TodoList,
  },
};
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
