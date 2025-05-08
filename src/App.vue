<template>
  <div class="container">
    <h1 class="title">Todo List</h1>

    <div class="input-group">
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Tambah kegiatan baru..." class="task-input" />
      <button @click="addTask" class="add-button">Tambah</button>
    </div>

    <div class="filter-group">
      <button @click="setFilter('all')" :class="{ active: filter === 'all' }">Semua</button>
      <button @click="setFilter('active')" :class="{ active: filter === 'active' }">Tampilkan yang sudah selesai</button>
      <button @click="setFilter('completed')" :class="{ active: filter === 'completed' }">Tampilkan yang belum selesai</button>
    </div>

    <ul class="task-list">
      <li v-for="(task, index) in filteredTasks" :key="index" :class="{ done: task.completed }">
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
import { ref, computed, onMounted } from 'vue'
import './style.css'

const newTask = ref('')
const tasks = ref([])
const filter = ref('all')


const initialTasks = [
  { text: 'Belajar Vue.js', completed: false },
  { text: 'Kerjakan tugas PBK', completed: true },
  { text: 'Baca dokumentasi GitHub', completed: false }
]

onMounted(() => {
  tasks.value = [...initialTasks]
})

function addTask() {
  if (newTask.value.trim()) {
    tasks.value.push({ text: newTask.value.trim(), completed: false })
    newTask.value = ''
  }
}

function removeTask(index) {
  tasks.value.splice(index, 1)
}

function setFilter(mode) {
  filter.value = mode
}

const filteredTasks = computed(() => {
  switch (filter.value) {
    case 'active':
      return tasks.value.filter(task => !task.completed)
    case 'completed':
      return tasks.value.filter(task => task.completed)
    default:
      return tasks.value
  }
})
</script>

