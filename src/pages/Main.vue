<template>
  <div id="board-page" class="page">
    <div id="board-container" class="row">
      <CategoryBoard 
        v-for= "(category, i) in categories"
        :key= "i"
        v-bind:tasks = "tasks"
        v-bind:category = "category"
        v-bind:color = "colors[i]"
        v-bind:lightercolor = "lightercolors[i]"
        v-bind:taskId = "taskId"
        v-on:toPage= "toPage"
        v-on:getTaskId = "getTaskId"
        v-on:moveTask = "moveTask"
        v-on:deleteTask = "deleteTask"
        v-on:selectCategory = "selectCategory"
        v-on:toEditPage = "toEditPage"
      ></CategoryBoard>
    </div>
  </div>
</template>

<script>
import CategoryBoard from '../components/CategoryBoard.vue'

export default {
  components: { CategoryBoard },
  name: "Main",
  data() {
    return {
      colors: ["salmon", "orange", "khaki", "springgreen"],
      lightercolors: ["peachpuff", "moccasin", "lemonchiffon", "rgb(220,255,200)"], 
      categories: ["backlog", "todo", "doing", "done"]
    }
  },
  props: ["tasks", "newTaskCategory", "taskId"],
  methods: {
    toPage(page) {
      this.$emit("toPage", page)
    },

    getAllTasks() {
      this.$emit("getAllTasks")
    },

    selectCategory(category) {
      this.$emit("selectCategory", category)
    },

    getTaskId(id) {
      this.$emit("getTaskId", id)
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


  },
  created() {
    this.getAllTasks()
  }
}
</script>

<style>

</style>