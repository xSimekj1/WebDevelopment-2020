<template>
  <div class="simple-form">
    <h1 v-if="created">{{ msg }}</h1>
    <form action="submit" class="simple-form__form">
      <div class="simple-form__item">
        <input
            ref="email"
            v-model="email"
            type="email"
            placeholder="email..."
        >
      </div>
      <div class="simple-form__item">
        <input
            ref="password"
            v-model="password"
            type="password"
            placeholder="heslo..."
        >
      </div>
      <div>
        <button>Skontroluj</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'SimpleForm',
  props: {
    msg: String
  },
  data() {
    return {
      email: null,
      password: null,
      created: null,
    }
  },
  methods: {
    submit() {
      console.log("Hello Svete")
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
