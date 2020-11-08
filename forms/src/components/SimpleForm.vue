<template>
  <div class="simple-form">
    <h1 v-if="created">{{ msg }}</h1>
    <form
        ref="form"
        action="submit"
        class="simple-form__form"
    >
      <div
          class="simple-form__head"
      >LOGIN</div>
      <div
          :class="{'simple-form__item--invalid': userExist,
                   'simple-form__item--success': userCreated
          }"
          class="simple-form__item"
      >
        <input
            ref="email"
            v-model="email"
            type="email"
            placeholder="email..."
            @change="userExist = null"
        >
        <div
            v-if="userExist"
            class="simple-form__error"
        >
          Používateľ s uvedením mailom je už registrovaný
        </div>
      </div>
      <div
          :class="{'simple-form__item--invalid': passwordErrors.length > 0,
                   'simple-form__item--success': userCreated
          }"
          class="simple-form__item"
      >
        <input
            ref="password"
            v-model="password"
            type="password"
            placeholder="heslo..."
        >
        <div v-if='passwordErrors.length > 0' class='hints'>
          <p
              v-for='(error, index) in passwordErrors'
              :key="index"
          >{{error}}</p>
        </div>
      </div>
      <div
          :class="{
              'simple-form__item--invalid': notSamePasswords,
              'simple-form__item--success': userCreated,
          }"
          class="simple-form__item">
        <input
            ref="checkPassword"
            v-model="checkPassword"
            type="password"
            placeholder="zopakuj heslo..."
        >
        <div
            v-if="notSamePasswords"
            class="simple-form__error"
        >
          Hesla sa nezhoduju
        </div>
      </div>
      <div
          :class="{'simple-form__item--success': userCreated}"
          class="simple-form__item"
      >
        <button @click.prevent="submit">Skontroluj</button>
      </div>
      <div
          v-if="submitted && userCreated"
          class="simple-form__output"
      >
        {{ email }} <br>
        {{ password }}
        <span class="simple-form__created">
          Registracia Uspesna
        </span>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'SimpleForm',
  props: {
    users: {
      type: Array,
      default: null,
    }
  },
  data() {
    return {
      email: '',
      password: '',
      checkPassword:'',
      created: false,
      submitted: false,
      formError: false,
      userCreated: false,
      userExist: false,
      rules: [
        { message:'One lowercase letter required.', regex:/[a-z]+/ },
        { message:"One uppercase letter required.",  regex:/[A-Z]+/ },
        { message:"8 characters minimum.", regex:/.{8,}/ },
        { message:"One number required.", regex:/[0-9]+/ }
      ],
    }
  },
  methods: {
    submit() {
      this.submitted = true;
      console.log('Email: ' + this.email + '\n' + 'Password: ' + this.password);
      console.log(this.$refs);
      let formValid = (this.passwordErrors.length > 0 && this.notSamePasswords) ? false : true;
      this.users.forEach(user => {
        if (user.email === this.$refs.email.value) {
          formValid = false;
        }
      })
      if (formValid) {
        this.userCreated = true;
      } else {
        this.userExist = true;
      }
      setTimeout(() => {
        this.submitted = false;
        this.userCreated = false;
      }, 2000)
    },
  },
  computed: {
    notSamePasswords () {
      if (this.passwordsFilled) {
        return (this.password !== this.checkPassword)
      } else {
        return false
      }
    },
    passwordErrors () {
      let errors = []
      for (let condition of this.rules) {
        if (!condition.regex.test(this.password)) {
          errors.push(condition.message)
        }
      }
      return errors;
    },
    passwordsFilled () {
      return (this.password !== '' && this.checkPassword !== '')
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less">
.simple-form {
  display: flex;
  justify-content: center;
}

.simple-form__head {
  margin-bottom: 30px;

  color: #2c3e50;
  font-size: 24px;
}

.simple-form__form {
  display: flex;
  flex-direction: column;

  width: 300px;
  padding: 30px 50px;


  border: 1px solid;
  border-radius: 4px;
}

.simple-form__item {
  display: flex;
  flex-direction: column;
  align-items: flex-start;

  margin-bottom: 16px;

  input {
    box-sizing: border-box;
  }

  input,
  button {
    padding: 8px 12px;
    width: 100%;
  }

  button {
    cursor: pointer;
  }
}

.simple-form__item--invalid {
  input {
      border: 1px solid red;
  }
}

.simple-form__error {
  margin-top: 8px;

  color: red;
  font-size: 12px;
}

.hints {
  text-align: start;
  p {
    color: red;
    font-size: 10px;
    margin: 8px 0;
  }
}

.simple-form__item--success {
  input {
    border: 1px solid green;
  }
  button {
    background-color: green;
    color: white;
  }
}

.simple-form__created {
  display: block;
  width: 100%;

  margin-top: 16px;

  font-size: 21px;
  color: green;
}

</style>
