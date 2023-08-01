<script>
import Task from './components/Task.vue';

  export default {
    data() {
      return {
        tasks: [],
        showForm: false,
        newTask : '',
      }
    },
    methods: {
      changeDone(id) {
        let task = this.tasks.filter((task) => task.id === id)[0];
        task.done = !task.done;
      },
      addTask() {
        this.showForm = true;
      },
      submitNewTask() {
        let newTask = {};
        newTask.task = this.newTask;
        if (this.tasks.length) {
          newTask.id = Math.max(...this.tasks.map((elem) => elem.id)) + 1;
        } else {
          newTask.id = 1;
        };
        this.tasks.push(newTask);
        this.newTask = '';
        this.showForm = false;
      },
      removeTask(id) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      },
      changeTask(id, newText) {
        let task = this.tasks.filter((task) => task.id === id)[0];
        task.task = newText;
      }
    },
    components: {
      Task,
    },
  }
</script>

<template>
  <div class="wrapper" v-if="tasks.length">
	<Task v-for="task in tasks"
    :key="task.id"
    :text="task.task"
    :done="task.done"
    :id="task.id"
    @changeDone="changeDone"
    @removeTask="removeTask"
    @changeTask="changeTask"
  />
  </div>
  <div v-if="showForm">
    <input type="text" v-model="newTask">
    <button @click="submitNewTask()">Добавить задачу</button>
  </div>
  <button @click="addTask()" v-if="!showForm">Добавить задачу</button>
</template>

<style>
div.wrapper {
  border: 1px solid black;
  width: max-content;
  padding: 5px;
}
</style>