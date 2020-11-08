<template>
  <div>
    <ul>
      <li v-for="(pizza, index) of localMenuFilter"
          :key="index"
      >
        <menu-item :pizza="pizza">

        </menu-item>
      </li>
    </ul>
    <input type="text" v-model="newPizzaName">
    <button @click="createPizza">New Pizza</button>
  </div>
</template>

<script>

import MenuItem from "@/components/MenuItem";
export default {
name: "PizzaMenu",
  components: {MenuItem},
  props: {
    menu:{
      type: Array,
      default: null,
    }
  },

  data(){
    return{
      localMenu: JSON.parse(JSON.stringify(this.menu)),
      newPizzaName: '',
    }
  },

  computed:{
    localMenuFilter(){
      return this.localMenu.filter(word => word.name !== "Hawai")
    },
  },

  methods:{
    createPizza(){
      const newPizza = {
        name: this.newPizzaName,
        price: 5,
        description: ['tomat'],
      }
      this.localMenu.push(newPizza)
      this.$emit("createPizza", newPizza)
    },

  }

}
</script>

<style scoped>

</style>