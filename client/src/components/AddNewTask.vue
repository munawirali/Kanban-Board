<template lang="html">
  <div class="modal fade" id="addTask" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
          <h4 class="modal-title" id="myModalLabel">Add Task</h4>
        </div>
        <form class="form-group">
          <div class="modal-body">
            <label>Title</label>
            <input v-model="task.title" type="text" class="form-control" placeholder="Title">
            <label>Description</label>
            <textarea v-model="task.description" name="name" rows="3" cols="80" class="form-control" placeholder="Description"></textarea>
            <!-- <input v-model="task.description" type="text" class="form-control" placeholder="Description"> -->
            <label>Point</label>
            <input v-model="task.point" type="text" class="form-control" placeholder="Point">
            <label>Assign To</label>
            <input v-model="task.assignTo" type="text" class="form-control" placeholder="Assign To">
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-primary" data-dismiss="modal">Close</button>
            <button @click="addTask(task)" type="button" class="btn btn-primary" data-dismiss="modal">Add Task</button>
          </div>
        </form>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
export default {
  props: ['task'],
  methods: {
    addTask (task) {
      this.$emit('emitAddTask', task)
    }
  }
}
</script>

<style lang="css">
</style>
