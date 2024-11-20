<script>
import Task from './components/Task.vue';

export default {
  name: 'App',
  components: {
    Task,
  },
  data() {
    return {
      tasks: [],
      filter: 'all'
    };
  },

  computed: {
    filteredTasks() {
      if(this.filter === 'active'){
        return this.tasks.filter((task) => !task.completed);
      }
      else if(this.filter === 'completed') {
        return this.tasks.filter((task) => task.completed);
      }
      return this.tasks;
    }
  },
  methods: {
   setFilter(filter) {
    this.filter = filter
   },
    clearAllTasks() {
      this.tasks = [];
    },
    addTask(newTask) {
      this.tasks.push(newTask);
    },
    deleteTask(taskId) {
      this.tasks = this.tasks.filter((task) => task.id !== taskId);
    },
    toggleTaskCompletion(taskId) {
      const task = this.tasks.find((task) => task.id === taskId);
      if (task) {
        task.completed = !task.completed;
      }
    },
  },
};
</script>

<template>
  <div id="app">
    <Task 
      v-bind:tasks="filteredTasks" 
      @set-filter="setFilter"
      @clear-all="clearAllTasks" 
      @add-task="addTask" 
      @delete-task="deleteTask" 
      @toggle-task="toggleTaskCompletion" 
    />
  </div>
</template>

<style scoped>
/* Add your global styles here */
</style>


