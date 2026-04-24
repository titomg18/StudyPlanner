<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import Navbar from './components/Navbar.vue'
import Sidebar from './components/Sidebar.vue'
import HomeView from './views/HomeView.vue'
import PlannerView from './views/PlannerView.vue'
import TasksView from './views/TasksView.vue'

const activeMenu = ref('dashboard')
const isMobile = ref(false)
const sidebarOpen = ref(false)

const checkMobile = () => {
  isMobile.value = window.innerWidth < 768
  if (!isMobile.value) sidebarOpen.value = true
  else sidebarOpen.value = false
}

const changeMenu = (menu) => {
  activeMenu.value = menu
  if (isMobile.value) sidebarOpen.value = false
}

const toggleSidebar = () => {
  if (isMobile.value) sidebarOpen.value = !sidebarOpen.value
}

const closeSidebar = () => {
  sidebarOpen.value = false
}

onMounted(() => {
  checkMobile()
  window.addEventListener('resize', checkMobile)
})
onUnmounted(() => window.removeEventListener('resize', checkMobile))
</script>

<template>
  <div class="app">
    <Navbar :isMobile="isMobile" @toggle-sidebar="toggleSidebar" />
    <div class="layout">
      <!-- Sidebar untuk desktop dan mobile drawer -->
      <transition name="slide">
        <Sidebar 
          v-if="sidebarOpen" 
          :active="activeMenu" 
          @menu-click="changeMenu"
          :isMobile="isMobile"
          @close="closeSidebar"
        />
      </transition>
      <!-- Overlay gelap untuk mobile -->
      <div v-if="isMobile && sidebarOpen" class="overlay" @click="closeSidebar"></div>
      <main class="content">
        <HomeView v-if="activeMenu === 'dashboard'" />
        <PlannerView v-if="activeMenu === 'planner'" />
        <TasksView v-if="activeMenu === 'tasks'" />
      </main>
    </div>
    <div v-if="isMobile && !sidebarOpen" class="bottom-nav">
      <button @click="changeMenu('dashboard')" :class="{ active: activeMenu === 'dashboard' }">🏠</button>
      <button @click="changeMenu('planner')" :class="{ active: activeMenu === 'planner' }">📅</button>
      <button @click="changeMenu('tasks')" :class="{ active: activeMenu === 'tasks' }">✅</button>
    </div>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: 'Segoe UI', system-ui, sans-serif;
  background: #fff5f7;
  height: 100vh;
  overflow: hidden;
}
.app {
  height: 100vh;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}
.layout {
  display: flex;
  flex: 1;
  overflow: hidden;
  position: relative;
}
.content {
  flex: 1;
  overflow-y: auto;
  padding: 20px;
  background: #fff5f7;
}
/* Animasi sidebar */
.slide-enter-active, .slide-leave-active {
  transition: transform 0.25s ease;
}
.slide-enter-from, .slide-leave-to {
  transform: translateX(-100%);
}
/* Overlay gelap untuk mobile */
.overlay {
  position: fixed;
  top: 60px;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0,0,0,0.4);
  z-index: 90;
}
.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(255,255,255,0.96);
  backdrop-filter: blur(12px);
  display: flex;
  justify-content: space-around;
  padding: 8px 12px;
  border-top: 1px solid #ffe0e7;
  z-index: 20;
}
.bottom-nav button {
  background: transparent;
  border: none;
  font-size: 1.5rem;
  padding: 6px 16px;
  border-radius: 40px;
  opacity: 0.5;
}
.bottom-nav button.active {
  opacity: 1;
  background: #ffe4ed;
  color: #db2777;
}
@media (min-width: 768px) {
  .content { padding: 28px; }
}
</style>