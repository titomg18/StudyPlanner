<template>
  <div class="tasks">
    <h2>✅ Daftar Tugas</h2>
    <p class="sub">Kelola tugas belajarmu dengan rapi</p>

    <div class="progress-container">
      <div class="progress-label">
        <span>{{ completedTasks }}/{{ tasks.length }} selesai</span>
        <span class="percent">{{ Math.round((completedTasks / tasks.length) * 100) }}%</span>
      </div>
      <div class="progress-bar">
        <div class="progress-fill" :style="{ width: `${(completedTasks / tasks.length) * 100}%` }"></div>
      </div>
    </div>

    <div class="task-list">
      <div v-for="task in tasks" :key="task.id" class="task-item">
        <input type="checkbox" v-model="task.done" :id="`task-${task.id}`" />
        <label :for="`task-${task.id}`" :class="{ done: task.done }">{{ task.name }}</label>
        <span class="due">{{ task.due }}</span>
      </div>
    </div>

    <button class="add-btn">+ Tambah Tugas Baru</button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const tasks = ref([
  { id: 1, name: 'Matematika - Integral', due: '24 Apr', done: true },
  { id: 2, name: 'Vue.js Components', due: '26 Apr', done: false },
  { id: 3, name: 'Reading TOEFL', due: '23 Apr', done: true },
  { id: 4, name: 'Laporan Proyek', due: '28 Apr', done: false }
])

const completedTasks = computed(() => tasks.value.filter(t => t.done).length)
</script>

<style scoped>
.tasks {
  max-width: 700px;
  margin: 0 auto;
}
.tasks h2 {
  font-size: 1.8rem;
  color: #be185d;
  margin-bottom: 4px;
}
.sub {
  color: #f472b6;
  margin-bottom: 24px;
}
.progress-container {
  background: white;
  border-radius: 28px;
  padding: 20px;
  margin-bottom: 28px;
  border: 1px solid #ffe0e7;
}
.progress-label {
  display: flex;
  justify-content: space-between;
  font-size: 0.85rem;
  margin-bottom: 8px;
  color: #831843;
}
.progress-bar {
  background: #ffe4ed;
  border-radius: 20px;
  height: 10px;
  overflow: hidden;
}
.progress-fill {
  background: #db2777;
  height: 100%;
  border-radius: 20px;
  transition: width 0.3s;
}
.task-list {
  background: white;
  border-radius: 28px;
  border: 1px solid #ffe0e7;
  overflow: hidden;
}
.task-item {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 16px 20px;
  border-bottom: 1px solid #ffe0e7;
}
.task-item:last-child {
  border-bottom: none;
}
.task-item input {
  width: 20px;
  height: 20px;
  accent-color: #db2777;
  cursor: pointer;
}
.task-item label {
  flex: 1;
  font-weight: 500;
  color: #4a044e;
  cursor: pointer;
}
.task-item .done {
  text-decoration: line-through;
  color: #f9a8d4;
}
.due {
  font-size: 0.75rem;
  background: #fff0f5;
  padding: 4px 12px;
  border-radius: 40px;
  color: #db2777;
}
.add-btn {
  width: 100%;
  margin-top: 24px;
  background: white;
  border: 2px dashed #fbcfe8;
  padding: 14px;
  border-radius: 60px;
  font-weight: 600;
  color: #db2777;
  cursor: pointer;
  transition: 0.2s;
}
.add-btn:hover {
  background: #fff0f5;
  border-color: #f9a8d4;
}
</style>