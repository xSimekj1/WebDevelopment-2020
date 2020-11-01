<template>
  <div class="pizza-card">
    <div class="pizza-card__head">
      <img src="https://via.placeholder.com/300x200" alt="pizzaImage">
    </div>
    <div class="pizza-card__body">
      <h2 class="pizza-card__name" v-text="pizza.name"/>
      <div class="pizza-card__description">
        <ul class="pizza-card__list">
          <li 
            v-for="(ingredient, index) of pizza.description" 
            :key="index"
            class="pizza-card__list-item"
            v-text="ingredient"
          />
        </ul>
      </div>
    </div>
    <div class="pizza-card__footer">
      <span v-text="'Cena: ' + pizza.price + ' €'"></span>
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

</style>
