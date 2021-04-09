<template>
  <div class="modal fade" id="move-task-modal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Select the New Category</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body d-flex justify-content-center">
          <select v-model= "updatedCategory" id="move-task-select">
            <option>backlog</option>
            <option>todo</option>
            <option>doing</option>
            <option>done</option>
          </select>
        </div>
        <div class="modal-footer">
          <button v-on:click="moveTask(updatedCategory)" type="button" data-bs-dismiss="modal" class="btn btn-primary mx-auto">Move</button>
        </div>
      </div>
    </div>
  </div> 
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      updatedCategory: "backlog"
    }
  },

  methods: {
    moveTask(newCategory) {
      this.$emit("moveTask", newCategory)
    }
  }
}
</script>

<style>

</style>