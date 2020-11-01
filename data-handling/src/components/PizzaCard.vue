<template>
  <div class="pizza-card">
    <div class="pizza-card__head">
      <img src="https://via.placeholder.com/300x200" alt="pizzaImage">
    </div>
    <div class="pizza-card__body">
      <h2 class="pizza-card__name" v-text="pizza.name"/>
      <div class="pizza-card__description">
        <ul>
          <li 
            v-for="(ingredient, index) of pizza.description" 
            :key="index"
            v-text="ingredient"
          />
        </ul>
      </div>
    </div>
    <div class="pizza-card__footer">
      <span v-text="pizza.price + ' €'"></span>
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

  border: 1px solid black;
}

</style>
