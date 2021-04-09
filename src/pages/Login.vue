<template>
  <div id="login-page" class= "page row">
    <div class="col-6 offset-3 text-center">
      <h2>Login</h2>

      <form id="login-form" v-on:submit.prevent="login">
        <div class="form-group">
          <label for="login-username">Username</label>
          <input v-model="username" type="text" class="form-control" id="login-username" aria-describedby="emailHelp" placeholder="Enter your username" required>
        </div>

        <div class="form-group">
          <label for="login-password">Password</label>
          <input v-model="password" type="password" class="form-control" id="login-password" placeholder="Enter your password" required>
        </div>

        <button id="login-button" type="submit" class="btn btn-primary">Login</button>
      </form>

      <p>Don't have an account yet? <a v-on:click.prevent="toPage('register')" href="">Register now!</a> </p>
      <p>Or login / register with your Google Account:</p>

    </div>
  </div> 
</template>

<script>
import axios from "../API/axios"

export default {
  name: "Login",


  data() {
    return {
      username: "",
      password: "",
    }
  },
  methods: {
    toPage(page) {
      this.$emit("toPage", page)
    },

    getUsername(username) {
      this.$emit("getUsername", username)
    },

    showError(message) {
      this.$emit("showError", message)
    },
    
    login() {
      axios({
        method: "POST",
        url: "/login",
        data: {
          username: this.username,
          password: this.password
        }
      })
      .then(response => {
        localStorage.setItem("access_token", response.data.access_token)
        localStorage.setItem("username", response.data.username)
        this.getUsername(response.data.username)
        this.toPage("board")
      })
      .catch(err => {
        this.showError(err.response.data.error)
      })
    },
  }
}
</script>

<style scoped>
  h2 {
    margin-bottom: 15px;
  }

  form{
    margin: 2em 0;
  }

  .form-group {
    margin: 1.5em 0;
  }
</style>