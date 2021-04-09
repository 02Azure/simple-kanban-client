<template>
  <div 
    v-bind:style="{ backgroundColor: taskcolor, borderLeft: `solid ${leftcolor} 8px`}" 
    v-on:dragstart= "getTaskId(task.id)"
    class="task"
    draggable="true"
    >
    <div class="task-nav-bar d-flex justify-content-between">
      <p class="task-due">{{task.due}}</p>
      <div class="icon-container">
        <i v-on:click="getTaskId(task.id)" data-bs-toggle="modal" data-bs-target="#move-task-modal" class="fa fa-arrows-alt-h"></i>
        <i 
          v-on:click="toEditPage(task.id)"
          class="fa fa-pencil-alt fa-xs"
        ></i> 
        <i 
          v-on:click="deleteTask(task.id)"
          class="fa fa-trash "
        ></i>
      </div>
    </div>          
    <p class="task-title">{{task.title}}</p>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: ["task", "color", "taskcolor", "leftcolor"],
  methods: {
    toEditPage(id) {
      this.$emit("toEditPage", id)
    },

    deleteTask(id) {
      this.$emit("deleteTask", id)
    },

    getTaskId(id) {
      this.$emit("getTaskId", id)
    }
  }
}
</script>

<style>

</style>