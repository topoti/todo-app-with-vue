<script setup>
import { computed, createApp, ref } from 'vue'
import Task from './components/Task.vue'

const tasks = ref([])
const filter = ref('all')

const filteredTasks = computed(() => {
  if (filter.value === 'active') {
    return tasks.value.filter((task) => !task.completed)
  } else if (filter.value === 'completed') {
    return tasks.value.filter((task) => task.completed)
  }
  return tasks.value
})

const setFilter = (newFilter) => {
      filter.value = newFilter
    };

const clearAllTasks = () => {
  tasks.value = []
}

const addTask = (newTask) => {
tasks.value.push(newTask)
}

const deleteTask = (taskId) => {
  tasks.value = tasks.value.filter((task) => task.id !== taskId)
}

const toggleTaskCompletion = (taskId) => {
const task = tasks.value.find((task) => task.id === taskId)
if(task) {
 task.completed = !task.completed 
}
}
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

</style>
