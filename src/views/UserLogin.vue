<template>
  <div>
    <form @submit.prevent="login">
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
        Login
      </button>

      <p>{{ error }}</p>

      Don't have an account?
      <router-link to="/register">
        Register
      </router-link>
    </form>
  </div>
</template>

<script>
export default {
  name: 'UserLogin',
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },

  methods: {
    login () {
      this.$store.dispatch('login', {
        email: this.email,
        password: this.password
      }).then(() => {
        this.$router.push({ name: 'dashboard' })
      }).catch(err => {
        this.error = err.response.data.error
      })
    }
  }
}
</script>
