<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <!-- Klasicky cyklus, pouzity priamo v HTML template, dynamicky generuje tvoju strukturu -->
        <div
          v-for="pizza in pizzas"
          :key="pizza.id"
          class="col col-1-4"
        >
        <span v-text="'<pizza-card>'"></span>
        <div class="card-wrapper">
          <pizza-card
            :pizza="pizza"
          />
        </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import data from './assets/data.json';
import PizzaCard from './components/PizzaCard.vue';

export default {
  name: 'App',
  components: {
    PizzaCard,
  },
  data() {
    return {
      pizzas: data.pizza,
    };
  },
};
</script>

<style lang="less">

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

ul {
  list-style-type: none;
}

li {
  text-decoration: none;
}

img {
  width: 100%;
  height: auto;
}

.row {
  display: flex;
  flex-wrap: wrap;
}

// Ukazka jednoduchej grid struktury
.col {
  display: flex;
  flex-direction: column;

  &-1-1 {
    flex: 0 0 100%;
    max-width: 100%;
  }

  &-1-2 {
    flex: 0 0 50%;
    max-width: 50%;
  }

  &-1-3 {
    flex: 0 0 33%;
    max-width: 33%;
  }

  &-1-4 {
    flex: 0 0 25%;
    max-width: 25%;
  }

  // Repsonzivita pre tablety a mobilne zariadenia
  @media only screen and (max-width: 768px) {
    max-width: 50%;
    flex: 0 0 50%;
  }

  @media only screen and (max-width: 450px) {
    max-width: 100%;
    flex: 0 0 100%;
  }
}

.card-holder {
  display: flex;
  flex-wrap: wrap;
}

.card-wrapper {
  display: flex;
  align-items: stretch;
  flex: 1 1 auto;
  margin: 10px;
}
</style>
