<script setup>
import { ref } from 'vue'

const newTask = ref('')
const tasks = ref([])

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push({ name: newTask.value.trim(), completed: false })
    newTask.value = ''
  }
}
</script>

<template>
<main class="container">
    <h1>Daftar Kegiatan</h1>
    <input v-model="newTask" placeholder="Tambah kegiatan..." class="input" />
    <button @click="addTask" class="btn-add">Tambah</button>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <input type="checkbox" v-model="task.completed" />
        <span :class="{ completed: task.completed }">{{ task.name }}</span>
      </li>
    </ul>
  </main>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
.completed {
  text-decoration: line-through;
  color: grey;
}
</style>
