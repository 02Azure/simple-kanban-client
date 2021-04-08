<template>
  <header class="row align-items-center">
    <h1 class="col-5">Kanban Board</h1>
    <nav v-if="page !== 'login' && page !== 'register'" class="col-4 offset-3">
      <ul class="list-unstyled list-inline">
        <li class="list-inline-item">{{this.username}}</li>
        <li class="list-inline-item">
          <a href="#" v-on:click="logout()">Logout</a>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  name: "Navbar",
  props: ["page", "username"],
  methods: {
    toPage(page) {
      this.$emit("toPage", page)
    },

    logout() {
      localStorage.clear()
      let auth2 = gapi.auth2.getAuthInstance();
      
      auth2.signOut().then(function () {
        console.log('User signed out.');
      });
      
      this.toPage("login")
    }
  }
}
</script>

<style>

</style>