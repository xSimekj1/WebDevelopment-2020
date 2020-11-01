<template>
  <div class="pizza-card">
    <!-- Template je pomocny tag v DOM ktory sa nevygeneruje ale sluzi nam napriklad pre vytvorenie rozhodovacej logiky -->
    <template v-if="!isNew">
      <div class="pizza-card__head">
        <img src="https://via.placeholder.com/300x200" alt="pizzaImage">
      </div>
      <div class="pizza-card__body">
        <h2 class="pizza-card__name" v-text="localPizza.name"/>
        <div class="pizza-card__description">
          <ul class="pizza-card__list">
            <!-- Vygeneruj mi pekne po jendom vsekty polozky v description -->
            <li 
              v-for="(ingredient, index) of localPizza.description" 
              :key="index"
              class="pizza-card__list-item"
              v-text="ingredient"
            />
            <li v-if="!editIngredients">
              <button @click="editIngredients = true">Pridať surovinu</button>
            </li>
            <li v-else>
              <div>
                <input type="text" v-model="newIngredient">
                <button @click="addIngredient()">+</button>
              </div>
            </li>
          </ul>
        </div>
      </div>
      <div class="pizza-card__footer">
        <!-- v-text prepisuje vnutro elementu textovym obsahom ktory mu posleme ako parameter -->
        <span v-text="`Cena: ${localPizza.price} € / ${pizzaChild.price} €`"></span>
      </div>
    </template>
    <!-- Ak povodna podmienka neplati vygeneruj tuto cast -->
    <template v-else>
      <div class="pizza-card__head">
        <button class="pizza-card__exit-button" @click="$emit('canceled')">x</button>
        <img src="https://via.placeholder.com/300x200" alt="pizzaImage">
      </div>
      <div class="pizza-card__body">
        <div 
          class="pizza-card__name"
          :class="{'pizza-card__name--input' : isNew}"
        >
          <input 
            v-model="newPizza.name" 
            type="text" 
            placeholder="Nova pizza..."
          >
        </div>
        <div class="pizza-card__description">
          <ul class="pizza-card__list">
            <li 
              v-for="(ingredient, index) of newPizza.description" 
              :key="index"
              class="pizza-card__list-item"
              v-text="ingredient"
            />
            <li v-if="!editIngredients">
              <button @click="editIngredients = true">Pridať surovinu</button>
            </li>
            <li v-if="editIngredients">
              <div>
                <input type="text" v-model="newIngredient">
                <button @click="addIngredient()">+</button>
              </div>
            </li>
          </ul>
        </div>
      </div>
      <div class="pizza-card__footer">
        <button @click="createPizza()">Pridať pizzu</button>
      </div>
    </template>
  </div>
</template>

<script>

export default {
  name: 'PizzaCard',
  // Props sú dáta ktoré nám do komponentu prichádzajú z rodicovskej komponenty.
  // Pouzivame ich vzdy tak ako nam prídu, nikdy ich nemenime v ramci komponenty.
  props: {
    pizza: {
      type: Object,
      default: null,
    },
    isNew: {
      type: Boolean,
      default: false,
    }
  },
  // Data sú data ktoré máme dostupné iba lokálne v ramci komponenty,
  // Mozeme s nimi lubovolne narabat a vykonavat nad nimi operacie a menit ich.
  data() {
    return {
      localPizza: null,
      editIngredients: false,
      newIngredient: '',
      newPizza: null,
    };
  },
  // Metoda ktora sa vola vzdy este predtym ako prvykrat vykresli data na obrazovku
  created() {
    this.init();
  },
  // Computed sú funkcie ktoré sa vyvolajú automaticky za behu aplikácie a reagujú na každú zmenu vyvolanú v komponente (podobne ako watcher)
  // Nepríjmajú parametre, uľahčujú prácu s dátami a pracujeme s nimi ako s ostatnými premennými.
  computed: {
    pizzaChild() {
      const pizzaChild = JSON.parse(JSON.stringify(this.localPizza));
      pizzaChild.price -= 3;
      return pizzaChild;
    }
  },
  // Methods sú funkcie ktoré sa vyvolajú pri manipulácií so stránkou (napr. používateľ klikne na tlačítko) 
  // Môžu príjímať parametre
  methods: {
    init() {
      if (this.pizza) {
        this.localPizza = JSON.parse(JSON.stringify(this.pizza));
      } else {
        this.newPizza = {
          name: '',
          price: '',
          description: ['tomat'],
        }
      }
    },
    addIngredient() {
      if(this.isNew) {
        this.newPizza.description.push(this.newIngredient);
      } else {
        this.localPizza.description.push(this.newIngredient);
        this.localPizza.price += 0.5;
        this.$emit('pizzaUpdated', this.localPizza);
      }
      this.newIngredient = null;
      this.editIngredients = false;
    },
    createPizza() {
      this.newPizza.price = this.newPizza.description.length + 3.5;
      this.$emit('pizzaCreated', this.newPizza);
      this.init();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less">
.pizza-card {
  display: flex;
  flex-direction: column;

  width: 300px;
  height: 100%;

  border: 1px solid black;
  border-radius: 10px;
}

.pizza-card__head {
  position: relative;

  height: 200px;
  width: 100%;

  img {
    width: 100%;
    height: auto;
    border-radius: 10px 10px 0 0;
  }
}

.pizza-card__body {
  display: flex;
  flex-direction: column;
}

.pizza-card__name {
  margin: 0;
  padding: 10px 0;
  border-bottom: 1px solid;
}

.pizza-card__name--input {
  padding: 8px 10px;

  input {
    max-width: 90%;

    font-size: 1.5em;
    font-weight: 700;
    text-align: center;
  }
}

.pizza-card__list {
  list-style: none;
  padding: 0;
}

.pizza-card__footer {
  display: flex;
  flex-grow: 1;
  justify-content: center;
  align-items: flex-end;
  padding-bottom: 5px;
}

.pizza-card__exit-button {
  position: absolute;
  right: 10px;
  top: 10px;
}

</style>
