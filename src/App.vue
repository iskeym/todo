<template>
<div class="app">
  <create-task v-model:show="dialogVisible" @create="createTask"/>
  <task-list :tasks="tasks" @remove="remove"/>
  <button class="plus" @click="showDialog">+</button>
</div>
</template>

<script>
import TaskList from '@/components/TasksList.vue'
import CreateTask from '@/components/CreateTask.vue'

export default {
  components: {
    TaskList,
    CreateTask
  },
  data() {
    return {
      tasks: [],
      dialogVisible: false
    }
  },
  methods: {
    remove(task) {
      this.tasks = this.tasks.filter(p => p.id !== task.id)
    },
    showDialog() {
      this.dialogVisible = true
    },
    createTask(task) {
      this.tasks.push(task)
      this.dialogVisible = false
    }
  },
  mounted() {
    if (localStorage.getItem('tasks')) {
      this.tasks = JSON.parse(localStorage.getItem('tasks'));
    }
  },
  watch: {
    tasks: {
      handler(newTasks) {
        localStorage.setItem('tasks', JSON.stringify(newTasks));
      },
      deep: true
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Fira+Sans:wght@300&display=swap');

body{
  font-family: 'Fira Sans', sans-serif;
}
.app{
  display: flex;
  flex-direction: column;
}
.plus{
  display: flex;
  margin-top: 50px;
  font-size: 20px;
  align-self: flex-end;
  padding: 20px 25px;
  border-radius: 100%;
  margin-right: 10%;
  border: 2px solid black;
  cursor: pointer;
  background: white;
  transition-property: all;
	transition-duration: 0.3s;
  &:hover{
    background: rgb(210, 210, 210);
  }
}
</style>
