<template>
  <main id="app">
    <TodoHeader msg="Vue Todo List!"/>
    <TodoList/>
    <TodoFooter author="Mathew Teague" msg="VueJS Todo list for a Textlocal coding test."/>
  </main>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {
  name: 'app',
  components: {
    TodoHeader,
    TodoList,
    TodoFooter,
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
  *{
    &:focus{
      outline-color: rgb(65, 184, 131);
    }
  }
}
</style>
