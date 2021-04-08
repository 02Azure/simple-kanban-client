<template>
  <div id="login-page" class= "page row">
    <div id ="login-form" class="col-6 offset-3 text-center">
      <h2>Login</h2>

      <form v-on:submit.prevent="login">
        <div class="form-group">
          <label for="login-username">Username</label>
          <input v-model="username" type="text" class="form-control" id="login-username" aria-describedby="emailHelp" placeholder="Enter your username" required>
        </div>
        <div class="form-group">
          <label for="login-password">Password</label>
          <input v-model="password" type="password" class="form-control" id="login-password" placeholder>
        </div> <br>

        <button id="login-button" type="submit" class="btn btn-primary">Login</button>
        <br><br>
        <p>Don't have an account yet? <a v-on:click.prevent="toPage('register')" href="">Register now!</a> Or login / register with your Google Account:</p>
        <div id="google-signin-button"></div>
      </form>

    </div>
  </div> 
</template>

<script>
import axios from "../API/axios"

export default {
  name: "Login",
  mounted() {
    gapi.signin2.render('google-signin-button', {
      onsuccess: this.onSignIn
    })
  },

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
        console.log(err.response.data.error)
      })
    },

    onSignIn(googleUser) {
      let id_token = googleUser.getAuthResponse().id_token;

      axios({
        method: "POST",
        url: "/glogin",
        data: {
          id_token
        }
      })
      .then(response => {
        console.log("berhasillogin")
        localStorage.setItem("access_token", response.data.access_token)
        localStorage.setItem("username", response.data.username)
        this.getUsername(response.data.username)
        this.toPage("board")
      })
      .catch(err => {
        console.log(err.response.data.error)
      })
    },
  }
}
</script>

<style>

</style>