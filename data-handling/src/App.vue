<template>
  <div id="app">
    <div class="gallery">
      <!-- Pre kazdu pizzu nam vytvori card-holder a v nom komponentu pizza-kard s jej vlastnymi datami -->
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
      <!-- Po vytvoreni vsetkych pizz vytvor este jednu ale teraz bez dat a s props isNew -->
      <div 
        class="card-holder"
      >
        <!-- @pizzaCreated, @canceled su nase vlastne eventy ktore sme si definovali v PizzaCard -->
        <pizza-card 
          v-if="createPizza" 
          isNew
          @canceled="createPizza = false"
          @pizzaCreated="pizzaCreated"
        />
        <!-- @click je nativny javascript event ktory sa zavola vzdy pri kliknuty na dany element -->
        <button v-else @click="createPizza = true">New pizza</button>
      </div>
    </div>
    <div class="list-menu">
      <pizza-menu :menu="pizzas" @createPizza="pizzaCreated"
      ></pizza-menu>

    </div>
  </div>
</template>

<script>
import data from './assets/data.json';

import PizzaCard from './components/PizzaCard.vue'
import PizzaMenu from "@/components/PizzaMenu";

export default {
  name: 'App',
  components: {
    PizzaMenu,
    PizzaCard
  },
  // App.vue je root komponent, nasa skutocna stranka ktoru vidime, vsetko ostatne je len obsah ktory sa v nom generuje
  // Root element nema props, pretoze mu ich nemame z kade poslat
  
  // Data sú data ktoré máme dostupné iba lokálne v ramci komponenty,
  // Mozeme s nimi lubovolne narabat a vykonavat nad nimi operacie a menit ich.
  data() {
    return {
      pizzas: data.pizza,
      createPizza: false,
    };
  },
  
  // Methods sú funkcie ktoré sa vyvolajú pri manipulácií so stránkou (napr. používateľ klikne na tlačítko) 
  // Môžu príjímať parametre
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

<style lang="less">
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
