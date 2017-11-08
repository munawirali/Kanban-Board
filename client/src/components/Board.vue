<template lang="html">
  <div class="container">
    <div class="row">
      <h1>Kanban</h1>
    </div>
    <AddNewTask :task=task @emitAddTask="addTask"></AddNewTask>
    <button @click="setBlankForm" type="button" name="button" class="btn btn-primary" data-toggle="modal" data-target="#addTask">Add New Task</button><br><br>
    <DetailTask :task="task" :id="task['.key']" @emitEditTask="updateNewStatus"></DetailTask>
    <div class="row">
      <div class="col-md-3">
        <div class="panel panel-danger">
          <div class="panel-heading">Back-Log</div>
          <div class="panel-body">
            <div v-for="task in backlog" class="panel panel-warning">
              <div class="panel-heading">{{ task.title }}</div>
              <div class="panel-body">
                Point : {{ task.point }}<br>
                AssignTo : {{ task.assignTo }}<br>
                <button @click="setDataTask(task['.key'])" type="button" name="button" class="btn btn-info" data-toggle="modal" data-target="#detilTask">Show Detil</button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-3">
        <div class="panel panel-info">
          <div class="panel-heading">Todo</div>
          <div class="panel-body">
            <div v-for="task in todo" class="panel panel-warning">
              <div class="panel-heading">{{ task.title }}</div>
              <div class="panel-body">
                Point : {{ task.point }}<br>
                AssignTo : {{ task.assignTo }}<br>
                <button @click="setDataTask(task['.key'])" type="button" name="button" class="btn btn-info" data-toggle="modal" data-target="#detilTask">Show Detil</button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-3">
        <div class="panel panel-success">
          <div class="panel-heading">Doing</div>
          <div class="panel-body">
            <div v-for="task in doing" class="panel panel-warning">
              <div class="panel-heading">{{ task.title }}</div>
              <div class="panel-body">
                Point : {{ task.point }}<br>
                AssignTo : {{ task.assignTo }}<br>
                <button @click="setDataTask(task['.key'])" type="button" name="button" class="btn btn-info" data-toggle="modal" data-target="#detilTask">Show Detil</button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-3">
        <div class="panel panel-primary">
          <div class="panel-heading">Done</div>
          <div class="panel-body">
            <div v-for="task in done" class="panel panel-warning">
              <div class="panel-heading">{{ task.title }}</div>
              <div class="panel-body">
                Point : {{ task.point }}<br>
                AssignTo : {{ task.assignTo }}<br>
                <button @click="setDataTask(task['.key'])" type="button" name="button" class="btn btn-info" data-toggle="modal" data-target="#detilTask">Show Detil</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AddNewTask from '@/components/AddNewTask'
import DetailTask from '@/components/DetailTask'
import * as firebase from 'firebase'
var config = {
  apiKey: 'AIzaSyAPIeGfcxUTmuNycu35RBJ6US0g2I-au2I',
  authDomain: 'new-kanban.firebaseapp.com',
  databaseURL: 'https://new-kanban.firebaseio.com',
  projectId: 'new-kanban',
  storageBucket: 'new-kanban.appspot.com',
  messagingSenderId: '947136798099'
}
const firebaseApp = firebase.initializeApp(config)
const db = firebaseApp.database()
const tasksRef = db.ref('tasks')

export default {
  components: {
    AddNewTask,
    DetailTask
  },
  firebase: {
    tasks: tasksRef
  },
  data () {
    return {
      task: {
        title: null,
        description: null,
        point: 0,
        assignTo: null,
        status: 0
      }
    }
  },
  methods: {
    addTask (task) {
      tasksRef.push(task)
    },
    updateNewStatus (params) {
      tasksRef.child(params.key)
      .child('status')
      .set(params.newStatus)
    },
    setBlankForm () {
      this.task.title = null
      this.task.description = null
      this.task.point = 0
      this.task.assignTo = null
    },
    setDataTask (key) {
      this.task = this.tasks.filter((task) => {
        return task['.key'] === key
      })[0]
    }
  },
  computed: {
    backlog () {
      return this.tasks.filter((task) => task.status === 0)
    },
    todo () {
      return this.tasks.filter((task) => task.status === 1)
    },
    doing () {
      return this.tasks.filter((task) => task.status === 2)
    },
    done () {
      return this.tasks.filter((task) => task.status === 3)
    }
  }
}
</script>

<style lang="css">
.container{
  width: 90%
}
h1{
  text-align: center;
  font-size: 50px;
  color: #07ac09
}
</style>
