<template>
  <div class="container">
    <h1 class="title">Todo List</h1>

    <div class="input-group">
      <input
        v-model="newTask"
        @keyup.enter="addTask"
        placeholder="Tambah kegiatan baru..."
        class="task-input"
      />
      <button @click="addTask" class="add-button">Tambah</button>
    </div>

    

    <ul class="task-list">
      <li
        v-for="(task, index) in filteredTasks"
        :key="index"
        :class="{ done: task.completed }"
      >
        <label>
          <input type="checkbox" v-model="task.completed" />
          <span class="task-text">{{ task.text }}</span>
        </label>
        <button @click="removeTask(index)" class="delete-button">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import './style.css'

const newTask = ref('')
const tasks = ref([])
const filter = ref('all')

function addTask() {
  if (newTask.value.trim()) {
    tasks.value.push({ text: newTask.value.trim(), completed: false })
    newTask.value = ''
  }
}

function removeTask(index) {
  tasks.value.splice(index, 1)
}


</script>
