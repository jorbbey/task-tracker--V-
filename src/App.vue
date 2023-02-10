<template>
  <div class="container">
    <AppHeader title="Task Tracker" @toggle-add-task="toggleAddTask" 
    :showAddTask ="showAddTask"/>
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <AppTask
      :tasks="tasks"
      @delete-task="deleteTask"
      @toggle-reminder="toggleReminder"
    />
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue'
import AppTask from './components/AppTask.vue'
import AddTask from './components/AddTask.vue'
export default {
  name: 'App',
  components: {
    AppHeader,
    AppTask,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },
  async created() {
    this.tasks = await this.fetchTasks()
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id) {
      if (confirm('Are You Sure?')) {
        this.tasks = this.tasks.filter((task) => task.id !== id)
        return this.tasks
      }
    },
    toggleReminder(id) {
        this.tasks = this.tasks.map((task) =>
          task.id === id ? { ...task, reminder: !task.reminder } : task,
          )
    },
    async fetchTasks() {
      const res = await fetch('api/tasks')

      const data = await res.json()
      return data   
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`)
      const data = await res.json()
      return data   
    },
  },
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
