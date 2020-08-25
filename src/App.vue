<template>
  <div id="app">
    <Logo />
    <Dropdown />
  </div>
</template>

<script>
import Logo from './components/Logo';
import Dropdown from './components/Dropdown';

export default {
  name: 'App',
  components: {
    Logo,
    Dropdown,
  }
}
</script>

<style>
@import "./assets/normalize.css";
@import url("https://fonts.googleapis.com/css2?family=Ubuntu:wght@400;700&display=swap");

* {
  box-sizing: border-box;
}

#app {
  font-family: Ubuntu, Helvetica, Arial, sans-serif;
  text-align: center;
  color: rgb(33, 37, 41);
}
</style>
