<template>
  <table class="table">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Title</th>
      <th scope="col">Priority</th>
      <th scope="col">Action</th>
    </tr>
  </thead>
  <tbody>
    <task v-for="(task, index) in tasks" :key ="index" :task = "task" :index = "index"></task>
    <tr>
      <td><input v-model="task.title" class="form-control" required type="text" id="task"></td>
      <td>
        <select v-model="task.priority" class="form-control" id="select">
          <option>Low</option>
          <option>Medium</option>
          <option>High</option>
        </select>
      </td>
      <td><button @click="store" class="btn btn-primary">Add</button></td>
    </tr>
  </tbody>
</table>
</template>

<script>
  import Task from "./Task.vue";

  export default {
    data(){
      return{
        tasks: [],
        task: {title: '', priority: ''}
      }
    },
    methods: {
      getTasks(){
        axios.get("/public/api/tasks")
        .then(response => {
          response.data.map(task => {
            this.tasks.push(task)
          })
        })
        .catch(e => {
           console.log(e)
        })
      },
      store(){
        axios.post("/public/api/tasks", this.task)
        .then(savedTask => {
          this.tasks.push(savedTask.data)
        })
      }
    },
    created(){
      this.getTasks()
    },
    components:{Task}
  }
</script>

<style lang="scss" scoped>

</style>
