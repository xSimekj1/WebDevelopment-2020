<template>
  <div id="app">
    <div class="gallery">
      <div 
        v-for="pizza in pizzas"
        :key="pizza.id"
        class="card-holder"
      >
        <pizza-card :pizza="pizza"/>
      </div>
    </div>
  </div>
</template>

<script>
import data from './assets/data.json';

import PizzaCard from './components/PizzaCard.vue'

export default {
  name: 'App',
  components: {
    PizzaCard
  },
  data() {
    return {
      pizzas: data.pizza,
    };
  },
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

.gallery {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  
  padding: 15px;
}

.card-holder {
  padding: 5px;
}
</style>
