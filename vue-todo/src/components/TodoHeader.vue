<template>
  <header>
    <h1>Vue Todo List!</h1>
    <input type="text"
      name="new-todo"
      id="newTodo"
      placeholder="Add a new item."
      autofocus
      v-model="newTodo"
      @keyup.enter="addTodo">
  </header>
</template>

<script>
export default {
  name: 'TodoHeader',
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  #newTodo{
    width: 100%;
    height: 80px;
  }
</style>
