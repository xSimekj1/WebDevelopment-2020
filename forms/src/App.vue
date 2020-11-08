<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <simple-form msg="Account succesfuly created!"/>
  </div>
</template>

<script>
import SimpleForm from './components/SimpleForm.vue'

export default {
  name: 'App',
  components: {
    SimpleForm
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
