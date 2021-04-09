<template>
  <div id="edit-page" class= "page row">
    <div id ="edit-form" class="col-8 offset-2 text-center">
      <h2>Edit this task</h2>
      <form v-on:submit.prevent="editTask()">
        <div class="form-group">
          <label for="title-edit">Title</label>
          <input v-model="title" type="text" class="form-control" id="title-edit" aria-describedby="emailHelp" placeholder="Enter the title of the Task" required>
        </div>
        <div class="form-group">
          <label for="edit-date">Due</label>
          <input v-model="due" type="date" class="form-control" id="edit-date" required>
        </div>
          <div class="row">
            <button type="submit" class="btn btn-primary col-5">Submit</button>
            <button v-on:click="toPage('board')" class="btn btn-danger col-5 offset-2">Cancel</button>
          </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Edit",
  data() {
    return {
      title: this.task.title,
      due: this.task.due
    }
  },
  props: ["task"],
  methods: {
    toPage(page) {
      this.$emit("toPage", page)
    },

    editTask() {
      let updatedTask = {
        title: this.title,
        due: this.due
      }

      this.$emit("editTask", updatedTask)
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
    margin: 2.5em 0;
  }
</style>