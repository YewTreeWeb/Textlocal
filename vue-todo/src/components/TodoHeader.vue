<template>
  <header>
    <img alt="Vue logo" src="../assets/logo.png" class="logo">
    <h1>{{ msg }}</h1>
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
  h1{
    font-size: 40px;
    text-transform: uppercase;
  }
</style>
