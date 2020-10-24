<template>
  <!-- BEM: pozri aj trello, sposob ako vytvaras jednoducho prepouzitelne komponenty -->
  <!-- CSS kopiruje strukturu dat -->
  <div class="pizza-card">
    <div class="pizza-card__image-wrapper">
      <img src="../assets/pizza.jpg" alt="pizza image" class="pizza-card__image">
    </div>
    <div class="pizza-card__body">
      <h2
        class="pizza-card__title"
        v-text="pizza.name"
      >
      </h2>
      <div class="pizza-card__description">
        <ul class="pizza-card__list">
          <!-- Klasicky cyklus, pouzity priamo v HTML template -->
          <!-- dynamicky generuje tvoju strukturu -->
          <li
            v-for="(ingedient, index) in pizza.description"
            :key="index"
            class="pizza-card__list-item"
          >
            {{ ingedient }}
          </li>
        </ul>
      </div>
      <div class="pizza-card__bottom">
        <!-- String literal: formatuje text s premennymi do spolocneho vystupneho retazca-->
        <span v-text="`Cena: ${pizza.price}€`"></span>
        <!-- BAD PRACTICE: manualne spajanie stringov-->
        <!-- <span v-text="'Cena:' + pizza.price + '€'"></span> -->
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PizzaCard',
  props: {
    pizza: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="less">
.pizza-card {
  padding: 16px;

  border-radius: 5px;
  box-shadow: 0px 5px 10px 0px rgba(0,0,0,0.75);
}

.pizza-card__title {
  color: #FFA69E;
  border-bottom: 1px solid #FFA69E;
  margin: 8px;
  padding-bottom: 16px;
}

.pizza-card__list {
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.pizza-card__list-item {
  margin: 4px;
  padding: 5px 10px;

  color: #ffffff;
  border: 1px solid #FFA69E;
  background: #FFA69E;
  border-radius: 15px;
}
</style>
