<template>
  <div class="container">
    <div class="task">
      <div class="title">
        <h1>To Do List</h1>
      </div>

      <!-- Form -->
      <div class="form">
        <input type="text" v-model="newTaskTitle" placeholder="New Task" @keyup.enter="handleAddTask"/>
        <button @click="handleAddTask">Add Item</button>
      </div>

      <!-- Task list -->
      <div class="taskItems">
        <ul>
          <li v-for="task in tasks" :key="task.id">
              <button @click="$emit('toggle-task', task.id)">
              <i :class="task.completed ? 'fas fa-check-circle' : 'far fa-circle'"></i>
              {{ task.title }}
            </button>
            <button @click="$emit('delete-task', task.id)">
              <i class="far fa-trash-alt"></i>
            </button>
          </li> 
        </ul>
      </div>

      <!-- Buttons -->
      <div class="clearBtns">
        <button @click="$emit('set-filter', 'active')">Active</button>
        <button @click="$emit('set-filter', 'all')">All</button>
        <button @click="$emit('set-filter', 'completed')">Completed</button>
        <button @click="$emit('clear-all')">Clear All</button>
      </div>

      <!-- Pending tasks -->
      <div class="pendingTask">
        <span>Pending Tasks: {{ pendingTasksCount }}</span>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Task',
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      newTaskTitle: '',
    };
  },
  computed: {
    pendingTasksCount() {
      return this.tasks.filter((task) => !task.completed).length;
    },
  },
  methods: {
    handleAddTask() {
      if (this.newTaskTitle.trim()) {
        this.$emit('add-task', {
          id: Date.now(),
          title: this.newTaskTitle,
          completed: false,
        });
        this.newTaskTitle = '';
      }
    },
  },
};
</script>

<style scoped>

</style>


