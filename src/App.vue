<template>
  <div id="app">
    <Login />
  </div>
</template>

<script>
import Login from "./components/UserLogin.vue";

export default {
  components: {
    Login,
  },
};
</script>

<style>
/* Global stil eklemeleri */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
