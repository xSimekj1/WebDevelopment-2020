<template>
  <div id="app">
    <simple-form :users="users"/>
  </div>
</template>

<script>
import data from './assets/data.json';
import SimpleForm from './components/SimpleForm.vue'

export default {
  name: 'App',
  components: {
    SimpleForm
  },
  data() {
    return {
      users: data.users,
    };
  },
}
</script>

<style>
#app {
  display: flex;
  justify-content: space-evenly;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
