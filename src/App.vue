<script setup>
import { computed, ref } from 'vue';
import Task from './components/Task.vue';
import Buttons from './components/Buttons.vue';

const tasks = ref([]);
const filter = ref('all');

const filteredTasks = computed(() => {
  if (filter.value === 'active') {
    return tasks.value.filter((task) => !task.completed);
  } else if (filter.value === 'completed') {
    return tasks.value.filter((task) => task.completed);
  }
  return tasks.value;
});

const setFilter = (newFilter) => {
  filter.value = newFilter;
};

const clearAllTasks = () => {
  tasks.value = [];
};

const addTask = (newTask) => {
  tasks.value.push(newTask);
};

const deleteTask = (taskId) => {
  tasks.value = tasks.value.filter((task) => task.id !== taskId);
};

const toggleTaskCompletion = (taskId) => {
  const task = tasks.value.find((task) => task.id === taskId);
  if (task) {
    task.completed = !task.completed;
  }
};
</script>

<template>
  <div id="app">
    <Task
      v-bind:tasks="filteredTasks"
      @add-task="addTask"
      @delete-task="deleteTask"
      @toggle-task="toggleTaskCompletion"
    />
    <Buttons 
      @set-filter="setFilter" 
      @clear-all="clearAllTasks" 
    />
  </div>
</template>

<style scoped>
#app {
  padding: 60px 0;
}
</style>
