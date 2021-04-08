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
        <button type="submit" class="btn btn-primary">Submit</button>
        <button v-on:click="toPage('board')" class="btn btn-danger">Cancel</button>
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

<style>

</style>