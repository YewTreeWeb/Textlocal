<template>
  <footer>
    <img alt="Vue logo" src="../assets/logo.png" class="logo-sm">
    <p class="copyright">&copy; Copyright by {{ author }} {{ date }} - {{ msg }}</p>
    <p class="references">
      Thanks to <a href="https://www.youtube.com/watch?v=A5S23KS_-bU&t=730s" target="_blank">Andre Madarang</a> and <a href="https://jsfiddle.net/yyx990803/4dr2fLb7/?utm_source=website&utm_medium=embed&utm_campaign=4dr2fLb7" target="_blank">yyx990803</a>
    </p>
  </footer>
</template>

<script>
import dayjs from 'dayjs';

export default {
  name: 'TodoFooter',
  props: {
    author: String,
    msg: String,
  },
  computed: {
    date: () => {
      const currentTime = new Date().getTime();
      const dateFormatted = dayjs(currentTime).format('DD/MM/YYYY');
      return dateFormatted;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  footer{
    margin-top: 100px;
    padding: 30px 15px;
  }
  .logo-sm{
    max-width: 90px;
    height: auto;
  }
</style>
