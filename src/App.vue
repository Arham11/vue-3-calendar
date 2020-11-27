<template>
  <calendar />
</template>

<script>
import calendar from "../src/components/Calendar";
export default {
  name: "App",
  components: {
    calendar
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 30px;
}
</style>
