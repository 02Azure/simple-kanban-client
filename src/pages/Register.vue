<template>
  <div id="register-page" class= "page row">
    <div id ="register-form" class="col-6 offset-3 text-center">
      <h2>Register</h2>

      <form v-on:submit.prevent="register()">
        <div class="form-group">
          <label for="reg-username">Username</label>
          <input v-model="username" type="text" class="form-control" id="reg-username" aria-describedby="emailHelp" placeholder="Fill with alphanumeric only" pattern="^[a-zA-Z0-9]+$" required title="alphanumeric only">
        </div>
        <div class="form-group">
          <label for="reg-email">Email</label>
          <input v-model="email" type="email" class="form-control" id="reg-email" aria-describedby="emailHelp" placeholder="example@mail.com" required>
        </div>
        <div class="form-group">
          <label for="reg-password">Password</label>
          <input v-model="password" type="password" class="form-control" id="reg-password" required>
        </div>
        <br>

        <button id="reg-button" type="submit" class="btn btn-primary">Register</button>
        <br><br>
        <p>Already have an account? <a v-on:click.prevent="toPage('login')" href="">Login with your current account now!</a></p>
      </form>

    </div>
  </div> 
</template>

<script>
import axios from "../API/axios"

export default {
  name: "Register",
  data() {
    return {
      username: "",
      email: "",
      password: ""
    }
  },
  methods: {
    toPage(page) {
      this.$emit("toPage", page)
    },
    register() {
      axios({
        method: "POST",
        url: "/register",
        data: {
          username: this.username,
          email: this.email,
          password: this.password
        }
      })
      .then(response => {
        this.toPage("login")
      })
      .catch(err => {
        Swal.fire({
          title: 'Oops...',
          text: err.response.data.error,
          imageUrl: 'https://streamsentials.com/wp-content/uploads/pepehands-transparent-pic.png',
          imageWidth: 200,
          imageAlt: 'Custom image',
        })
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