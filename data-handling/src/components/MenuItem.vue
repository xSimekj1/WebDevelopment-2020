<template>
  <div class="menu-item">
    <button @click="discount">Zlava</button>
    <h1 v-text="pizza.name"></h1>
    <p v-for="(ingredient, index) of localPizza.description"
      :key="index"
       v-text="ingredient"
       @click="removeIngredient(index)"
    ></p>
    <input type="text" v-model="newIngredient">
    <button @click="addNewIngredient">pridaj</button>
    <p>{{localPizza.price}} / {{pizzaChild}}</p>

  </div>
</template>

<script>
export default {
name: "MenuItem",
  props:{
    pizza:{
      type: Object,
      default: null,
    }
  },

  data(){
    return {
      localPizza: JSON.parse(JSON.stringify(this.pizza)),
      newIngredient: '',
    }
  },


  computed: {
    pizzaChild(){
      var price = this.localPizza.price;
      return price - 3
    }
  },

  methods:{
    discount(){
      this.localPizza.price -= 2
    },
    addNewIngredient(){
      this.localPizza.description.push(this.newIngredient)
    },
    removeIngredient(index){
      this.localPizza.description.splice(index, 1)
    }
  },

  watch:{
    pizza:{
      handler(newValue){
        this.localPizza = newValue
      },
      deep: true,
    }
  }

}
</script>

<style scoped>

.menu-item{
  display: flex;
  align-items: center;
}

</style>