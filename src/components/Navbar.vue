<template>
  <header class="row align-items-center">
    <h1 class="col-7 col-md-5">Kanban Board</h1>
    <nav v-if="page !== 'login' && page !== 'register'" class="col-5 col-md-3, offset-md-2">
      <ul class="list-unstyled list-inline">
        <li class="list-inline-item">{{this.username}}</li>
        <li class="list-inline-item">
          <a href="#" v-on:click.prevent="logout()">Logout</a>
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
      let thisToPage = this.toPage
      let auth2 = gapi.auth2.getAuthInstance();
      
      localStorage.clear()

      auth2.signOut()
        .then(function () {
        console.log('User signed out.');
      
        thisToPage("login")
      })
    }
  },

  mounted() {
    console.log("mounted navbar gapi")
        console.log(gapi)
  }
}
</script>

<style>

</style>