<template>
  <div id="app">
    <Games />
  </div>
</template>

<script>
import Games from "./components/Games.vue";

export default {
  name: "App",
  components: {
    Games
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
  background: #000;
}
body,
html {
  background: #000;
}
</style>
