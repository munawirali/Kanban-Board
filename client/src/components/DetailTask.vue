<template lang="html">
  <div class="modal fade" id="detilTask" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
          <h4 class="modal-title" id="myModalLabel">{{ task.title }}</h4>
        </div>
        <form class="form-group">
          <div class="modal-body">
            <label>Description : </label><br>
            <label>{{ task.description }}</label><br><br>
            <label>Point : </label><br>
            <label>{{ task.point }}</label><br><br>
            <label>Assign To : </label><br>
            <label>{{ task.assignTo }}</label><br><br>
          </div>
          <div class="modal-footer">
            <button :disabled="task.status === 0" @click="setAction({newStatus: task.status-1, key: task['.key']})" type="button" class="btn btn-primary" data-dismiss="modal">Previous</button>
            <button type="button" class="btn btn-primary" data-dismiss="modal">Close</button>
            <button :disabled="task.status === 3" @click="setAction({newStatus: task.status+1, key: task['.key']})" type="button" class="btn btn-primary" data-dismiss="modal">Next</button>
          </div>
        </form>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
export default {
  props: ['task', 'id'],
  methods: {
    setAction (params) {
      this.$emit('emitEditTask', params)
    }
  },
  mounted () {
    // let task =
  }
}
</script>

<style lang="css">
</style>
