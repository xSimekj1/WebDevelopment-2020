<template>
  <div>
    {{ pizzaLocal.name }}
    {{ priceExtra }}
  </div>
</template>

<script>
export default {
  name: 'PizzaListItem',
  props: {
    pizza: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      pizzaLocal: this.pizza,
    };
  },
  computed: {
    priceExtra() {
      return parseInt(this.pizzaLocal.price, 10) + 2;
    },
  },
};
</script>

<style scoped>

</style>
