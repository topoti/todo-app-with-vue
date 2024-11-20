<template>
  <div class="container">
    <div class="task">
      <div class="title">
        <h1>To Do List</h1>
      </div>

      <!-- Form -->
      <div class="form">
        <input type="text" v-model="newTaskTitle" placeholder="What needs to be done" @keyup.enter="handleAddTask"/>
        <button @click="handleAddTask">Add Item</button>
      </div>

      <!-- Task list -->
      <div class="taskItems">
        <ul>
          <li v-for="task in tasks" :key="task.id">
              <button @click="emit('toggle-task', task.id)">
              <i :class="task.completed ? 'fas fa-check-circle' : 'far fa-circle'"></i>
              {{ task.title }}
            </button>
            <button @click="emit('delete-task', task.id)">
              <i class="far fa-trash-alt"></i>
            </button>
          </li> 
        </ul>
      </div>

      <!-- Buttons -->
      <div class="clearBtns">
        <button @click="emit('set-filter', 'active')">Active</button>
        <button @click="emit('set-filter', 'all')">All</button>
        <button @click="emit('set-filter', 'completed')">Completed</button>
        <button @click="emit('clear-all')">Clear All</button>
      </div>

      <!-- Pending tasks -->
      <div class="pendingTask">
        <span>Pending Tasks: {{ pendingTasksCount }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { defineProps, defineEmits } from 'vue';
const props = defineProps({
  tasks: {
    type: Array,
    required: true
  }
})

const emit = defineEmits([
  'set-filter', 'clear-all', 'add-task', 'delete-task', 'toggle-task'
])

const newTaskTitle = ref('')
const pendingTasksCount = computed(() => {
  return props.tasks.filter((task) => !task.completed).length;
})

const handleAddTask = () => {
  if (newTaskTitle.value.trim()) {
        emit('add-task', {
          id: Date.now(),
          title: newTaskTitle.value,
          completed: false,
        });
        newTaskTitle.value = '';
      }
}
</script>

<style scoped>

</style>


