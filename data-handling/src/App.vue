<template>
  <div id="app">
    <div class="gallery">
      <div 
        v-for="pizza in pizzas"
        :key="pizza.id"
        class="card-holder"
      >
        <pizza-card 
          :pizza="pizza"
          @pizzaUpdated="pizzaUpdated"
        />
      </div>
      <div 
        class="card-holder"
      >
        <pizza-card 
          v-if="createPizza" 
          isNew
          @canceled="createPizza = false"
          @pizzaCreated="pizzaCreated"
        />
        <button v-else @click="createPizza = true">New pizza</button>
      </div>
    </div>
    <div class="list-menu">
      TODO
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
      createPizza: false,
    };
  },
  methods: {
    pizzaCreated(event) {
      this.pizzas.push(event)
    },
    pizzaUpdated(event) {
      let index = this.pizzas.findIndex(pizza => pizza.id === event.id);
      this.pizzas[index].description = event.description;
      this.pizzas[index].price = event.price;
    }
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
}

h2 {
  margin: 0;
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
