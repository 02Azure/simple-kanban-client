<template>
  <div id="add-page" class= "page row">
    <div id ="add-form" class="col-8 offset-2 text-center">
      <h2>Add a New Task to {{newTaskCategory}} category</h2>
      <form v-on:submit.prevent="addNewTask()">
        <div class="form-group">
          <label for="title-add">Title</label>
          <input v-model="title" type="text" class="form-control" id="title-add" aria-describedby="emailHelp" placeholder="Enter the title of the new Task" required>
        </div>
        <div class="form-group">
          <label for="add-date">Due</label>
          <input v-model="due" type="date" class="form-control" id="add-date" required>
        </div>
          <div class="row">
            <button type="submit" class="btn btn-primary col-5">Add</button>
            <button v-on:click="toPage('board')" class="btn btn-danger col-5 offset-2">Cancel</button>
          </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Add",
  data() {
    return {
      title: "",
      due: ""
    }
  },
  props: ["tasks", "newTaskCategory"],
  methods: {
    toPage(page) {
      this.$emit("toPage", page)
    },

    addNewTask() {
      let newTask = {
        title: this.title,
        due: this.due,
        category: this.newTaskCategory
      }

      this.$emit("addNewTask", newTask)
    }
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

  button {
    margin:0 10px;
    width: 45%
  }
</style>