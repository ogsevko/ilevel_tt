<template>
  <div id="app">
    <Logo />
  </div>
</template>

<script>
import Logo from './components/Logo';

export default {
  name: 'App',
  components: {
    Logo
  }
}
</script>

<style>
@import "./assets/normalize.css";
@import url("https://fonts.googleapis.com/css2?family=Ubuntu:wght@400;700&display=swap");

#app {
  font-family: Ubuntu, Helvetica, Arial, sans-serif;
  text-align: center;
  color: rgb(33, 37, 41);
}
</style>
