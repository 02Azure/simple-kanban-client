<template>
  <div 
    v-on:drop="selectCategory(category); moveTask(category)"
    v-on:dragenter.prevent
    v-on:dragover.prevent
    class="category-board col-xl-3 col-md-6 col-12"
    >
    <div v-bind:style="{ backgroundColor: color}" class="category-title-bar d-flex justify-content-between align-items-center">
      <h2 class="category-title" v-text="Cap1stLetterCategory"></h2>
      <i v-on:click="selectCategory(category); toPage('add')" class="fa fa-plus fa-lg"></i>
    </div>

    <div class="tasks-container">
      <Task
        v-for="task in filteredTasks"
        :key="task.id"
        v-bind:task= "task"
        v-bind:taskId = "taskId"
        v-bind:leftcolor = "color"
        v-bind:taskcolor = "lightercolor"
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
  props: ["category", "tasks", "taskId", "color", "lightercolor"],
  methods: {
    toPage(page) {
      this.$emit("toPage", page)
    },

    selectCategory(category) {
      this.$emit("selectCategory", category)
    },
    
    toEditPage(id) {
      this.$emit("toEditPage", id)
    },

    moveTask(category) {
      this.$emit("moveTask", category)
    },

    deleteTask(id) {
      this.$emit("deleteTask", id)
    },

    getTaskId(id) {
      this.$emit("getTaskId", id)
    }
  },
  computed: {
    filteredTasks() {
      return this.tasks.filter(task => task.category === this.category)
    },

    Cap1stLetterCategory() {
      return this.category[0].toUpperCase() + this.category.slice(1)
    }
  },
  components: {Task}

}
</script>

<style>

</style>