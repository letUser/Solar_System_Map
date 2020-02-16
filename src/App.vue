<template>
  <div id="app">
    <Header />
  </div>
</template>

<script>
import Header from "./components/header.vue";

export default {
  name: "App",
  components: {
    Header
  }
};
</script>

<style>
body {
  margin: 0;
  background-color: url(~@/assets/space.jpg);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
