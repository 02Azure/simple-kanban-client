<template>
  <div class="container">
    <Navbar 
      v-bind:page = "page"
      v-bind:username = "username"
      v-on:toPage = "toPage"
    ></Navbar>

    <Login 
      v-if="page ==='login'"
      v-on:toPage = "toPage"
      v-on:getUsername = "getUsername"
    ></Login>

    <Register 
      v-if="page ==='register'"
      v-on:toPage = "toPage"
      v-on:register = "register"
    ></Register>

    <Main
      v-else-if="page === 'board'"
      v-bind:tasks = "tasks"
      v-bind:taskId = "taskId"
      v-on:getAllTasks= "getAllTasks"
      v-on:getTaskId = "getTaskId"
      v-on:selectCategory = "selectCategory"
      v-on:toEditPage = "toEditPage"
      v-on:moveTask = "moveTask"
      v-on:deleteTask= "deleteTask"
    ></Main>
        
    <Add
      v-else-if="page ==='add'"
      v-bind:tasks = "tasks"
      v-bind:newTaskCategory = "newTaskCategory"
      v-on:toPage = "toPage"
      v-on:addNewTask = "addNewTask"
    ></Add>

    <Edit
      v-else-if="page ==='edit'"
      v-bind:task = "findOne"
      v-on:toPage = "toPage"
      v-on:editTask = "editTask"
    ></Edit>

    <Modal
      v-on:moveTask = "moveTask"
    ></Modal>
  </div>
</template>

<script>
import Navbar from "./components/Navbar"
import Modal from "./components/Modal"
import Login from "./pages/Login"
import Register from "./pages/Register"
import Main from "./pages/Main"
import Add from "./pages/Add"
import Edit from "./pages/Edit"
import axios from "../src/API/axios"

export default {
  name: "App",
  components: {Navbar, Modal, Login, Register, Main, Add, Edit},
  data() {
    return{
      page: "login",
      username: localStorage.getItem("username"),
      tasks: [],
      taskId: 0,
      newTaskCategory: ""
    }
    
  },
  methods: {
    toPage(newPage) {
      this.page = newPage
    },

    selectCategory(category) {
      this.newTaskCategory = category
      this.toPage("add")
    },

    toEditPage(id) {
      this.taskId = id
      this.toPage("edit")
    },

    register(input) {
      console.log(input)
    },

    getUsername(username) {
      this.username = username
    },

    getTaskId(id) {
      this.taskId = id
    },

    getAllTasks() {
      axios({
        url: "/tasks",
        method: "GET",
        headers: {
          access_token: localStorage.getItem("access_token")
        }
      })

      .then(response => {
        this.tasks = response.data
      })

      .catch(err => {
        console.log(err.response.data.error)
      })
    },
    
    addNewTask(newTask) {
      axios({
        url: "/tasks",
        method: "POST",
        headers: {
          access_token: localStorage.getItem("access_token")
        },
        data: {
          title: newTask.title,
          due: newTask.due,
          category: newTask.category
        }
      })

      .then(response => {
        this.toPage("board")
      })
      
      .catch(err => {
        console.log(err.response.data.error)
      })
    },

    editTask(updatedTask) {
      axios({
        url: "/tasks/" + this.taskId,
        method: "PUT",
        headers: {
          access_token: localStorage.getItem("access_token")
        },
        data: {
          title: updatedTask.title,
          due: updatedTask.due
        }
      })

      .then(response => {
        this.toPage("board")
      })
      
      .catch(err => {
        console.log(err.response.data.error)
      })
    },

    moveTask(newCategory) {
      console.log(this.taskId, newCategory)
      axios({
        url: "/tasks/" + this.taskId,
        method: "PATCH",
        headers: {
          access_token: localStorage.getItem("access_token")
        },
        data: {
          category: newCategory
        }
      })

      .then(response => {
        this.getAllTasks()
      })
      
      .catch(err => {
        console.log(err.response.data.error)
      })
    },

    deleteTask(id) {
      axios({
        url: "/tasks/" + id,
        method: "DELETE",
        headers: {
          access_token: localStorage.getItem("access_token")
        }
      })

      .then(response => {
        this.getAllTasks()
      })
      
      .catch(err => {
        console.log(err.response.data.error)
      })
    }
  },
  computed: {
    findOne() {
      return this.tasks.find(task => task.id === this.taskId)
    }
  },

  created() {
    if(localStorage.getItem("access_token")) this.page = "board"
  }
}
</script>

<style>

</style>