<template>
  <div>
    <form @submit.prevent="register">
      <label for="name">Name:</label>
      <input
        id="name"
        v-model="name"
        type="text"
        name="name"
        value
      >

      <label for="email">Email:</label>
      <input
        id="email"
        v-model="email"
        type="text"
        name="email"
        value
      >

      <label for="password">Password:</label>
      <input
        id="password"
        v-model="password"
        type="password"
        name="password"
        value
        autocomplete="on"
      >

      <button type="submit">
        Register
      </button>

      <ul>
        <li v-for="(error, index) in errors" :key="index">
          {{ error }}
        </li>
      </ul>

      Already have an account?
      <router-link to="/login">
        Login
      </router-link>
    </form>
  </div>
</template>

<script>
export default {
  name: 'RegisterUser',

  data () {
    return {
      name: '',
      email: '',
      password: '',
      errors: null
    }
  },
  methods: {
    register () {
      this.$store.dispatch('register', {
        name: this.name,
        email: this.email,
        password: this.password
      })
        .then(() => {
          this.$router.push({ name: 'dashboard' })
        })
        .catch(err => {
          this.errors = err.response.data.errors
        })
    }
  }
}
</script>

<style scoped>

</style>
