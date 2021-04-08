<template>
  <div class="category-board col-3">
    <div class="category-title-bar d-flex justify-content-between align-items-center">
      <h2 class="category-title" v-text="category[0].toUpperCase() + category.slice(1)"></h2>
      <i v-on:click="selectCategory(category)" class="fa fa-plus fa-lg"></i>
    </div>

    <div class="tasks-container">
      <Task
        v-for="task in filterCategory"
        :key="task.id"
        v-bind:task= "task"
        v-bind:taskId = "taskId"
        v-on:getTaskId = "getTaskId"
        v-on:deleteTask = "deleteTask"
        v-on:toEditPage = "toEditPage"
      ></Task>
    </div>



  </div>
</template>

<script>
import Task from "./Task"

export default {
  name: "CategoryBoard",
  props: ["category", "tasks", "taskId"],
  methods: {
    selectCategory(category) {
      this.$emit("selectCategory", category)
    },
    
    toEditPage(id) {
      this.$emit("toEditPage", id)
    },

    deleteTask(id) {
      this.$emit("deleteTask", id)
    },

    getTaskId(id) {
      this.$emit("getTaskId", id)
    }
  },
  computed: {
    filterCategory() {
      return this.tasks.filter(task => task.category === this.category)
    },
  },
  components: {Task}

}
</script>

<style>

</style>