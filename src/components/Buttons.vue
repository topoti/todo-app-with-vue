<script setup>
import { defineEmits } from 'vue'

const emit = defineEmits(['set-filter', 'clear-all'])

const handleSetFilter = (filter) => {
  emit('set-filter', filter)
}

const handleClearAll = () => {
  emit('clear-all')
}
</script>

<template>
  <div class="container">
    <div class="allButtons">
      <div class="clearBtns">
        <button @click="handleSetFilter('active')">Active</button>
        <button @click="handleSetFilter('all')">All</button>
        <button @click="handleSetFilter('completed')">Completed</button>
        <button @click="handleClearAll">Clear All</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.allButtons {
  margin-top: 20px;
  margin-left: 80px;
}
.clearBtns {
  display: flex;
  justify-content: space-between;
  margin: 0 0 20px;
}

.clearBtns button {
  width: 100%;
  background: blueviolet;
  color: #fff;
  border: none;
  border-radius: 10px;
  padding: 10px;
  margin: 0 5px;
}

.clearBtns button:hover {
  background: #333;
}

.clearBtns button:focus {
  background: green;
}
</style>
