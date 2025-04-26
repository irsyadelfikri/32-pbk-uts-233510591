<script setup>
import { ref, computed } from 'vue'

const newTask = ref('')
const tasks = ref([])

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push({ name: newTask.value.trim(), completed: false })
    newTask.value = ''
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}

const showOnlyIncomplete = ref(false)

const filteredTasks = computed(() => {
  if (showOnlyIncomplete.value) {
    return tasks.value.filter(task => !task.completed)
  }
  return tasks.value
})
</script>

<template>
<main class="container">
    <h1>Daftar Kegiatan</h1>
    <input v-model="newTask" placeholder="Tambah kegiatan..." class="input" />
    <button @click="addTask" class="btn-add">Tambah</button>
    <ul>
      <li v-for="(task, index) in filteredTasks" :key="index">
        <input type="checkbox" v-model="task.completed" />
        <span :class="{ completed: task.completed }">{{ task.name }}</span>
        <button @click="deleteTask(index)" class="btn-delete">Batalkan</button>
      </li>
    </ul>
<div class="filter">
  <label><input type="checkbox" v-model="showOnlyIncomplete" /> Tampilkan hanya yang belum selesai</label>
</div>
  </main>
</template>

<style scoped>
.page-background {
  background-color: #f0f2f5;
  min-height: 100vh;
  width: 100%;
  padding: 20px 0;
}

.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 2rem;
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.1);
  font-family: 'Inter', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

h1 {
  text-align: center;
  color: #3a3a3a;
  margin-bottom: 1.5rem;
  font-weight: 600;
}

.input-group {
  display: flex;
  margin-bottom: 1rem;
  gap: 15px;
}

.input {
  flex: 1;
  padding: 12px 15px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 1rem;
  outline: none;
  transition: border-color 0.3s, box-shadow 0.3s;
}

.input:focus {
  border-color: #4d7cfe;
  box-shadow: 0 0 0 3px rgba(77, 124, 254, 0.2);
}

.btn-add {
  background-color: #4d7cfe;
  color: white;
  border: none;
  border-radius: 8px;
  padding: 12px 20px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.2s;
}

.btn-add:hover {
  background-color: #3a68e0;
  transform: translateY(-2px);
}

.btn-add:active {
  transform: translateY(0);
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 1.5rem 0;
}

li {
  display: flex;
  align-items: center;
  padding: 12px 15px;
  background-color: white;
  border-radius: 8px;
  margin-bottom: 10px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
  transition: transform 0.2s, box-shadow 0.2s;
}

li:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

li input[type="checkbox"] {
  margin-right: 12px;
  width: 18px;
  height: 18px;
  cursor: pointer;
  accent-color: #4d7cfe;
}

li span {
  flex: 1;
  font-size: 1rem;
  color: #333;
  transition: color 0.3s, text-decoration 0.3s;
}

.completed {
  text-decoration: line-through;
  color: #8a8a8a !important;
}

.btn-delete {
  background-color: #ff5252;
  color: white;
  border: none;
  border-radius: 6px;
  padding: 8px 12px;
  cursor: pointer;
  transition: background-color 0.3s;
  font-size: 0.9rem;
}

.btn-delete:hover {
  background-color: #e04141;
}

.filter {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
  font-size: 0.9rem;
  color: #666;
}

.filter input[type="checkbox"] {
  margin-right: 8px;
  cursor: pointer;
  accent-color: #4d7cfe;
}

@media (max-width: 640px) {
  .container {
    padding: 1.5rem;
    margin: 0 1rem;
  }
  
  .input-group {
    flex-direction: column;
    gap: 10px;
  }
  
  .btn-add {
    width: 100%;
  }
  
  li {
    flex-wrap: wrap;
  }
  
  .btn-delete {
    margin-left: auto;
  }
}
.completed {
  text-decoration: line-through;
  color: grey;
}
</style>