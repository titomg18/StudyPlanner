<script setup>
const props = defineProps({ active: String, isMobile: Boolean })
const emit = defineEmits(['menuClick', 'close'])

const menus = [
  { id: 'dashboard', label: 'Dashboard', icon: '🏠' },
  { id: 'planner', label: 'Planner', icon: '📅' },
  { id: 'tasks', label: 'Tugas', icon: '✅' }
]

const handleClick = (id) => {
  emit('menuClick', id)
  if (props.isMobile) emit('close')
}
</script>

<template>
  <aside class="sidebar" :class="{ 'mobile-sidebar': isMobile }">
    <!-- Tombol close khusus mobile -->
    <button v-if="isMobile" class="close-btn" @click="emit('close')">✕</button>
    <div class="profile">
      <div class="avatar-icon">🎀</div>
      <h4>Belajar Yuk!</h4>
      <p>Target hari ini: 3 topik</p>
    </div>
    <nav class="nav">
      <div 
        v-for="item in menus" 
        :key="item.id" 
        class="nav-item"
        :class="{ active: active === item.id }"
        @click="handleClick(item.id)"
      >
        <span class="nav-icon">{{ item.icon }}</span>
        <span>{{ item.label }}</span>
      </div>
    </nav>
    <div class="footer">✨ #StayConsistent ✨</div>
  </aside>
</template>

<style scoped>
/* Sidebar desktop */
.sidebar {
  width: 260px;
  background: white;
  border-right: 2px solid #ffe0e7;
  display: flex;
  flex-direction: column;
  padding: 20px 0;
  height: 100%;
  position: relative;
  flex-shrink: 0;
}
/* Sidebar mobile: lebar 85% dari kiri, penuh dari atas ke bawah */
.mobile-sidebar {
  position: fixed;
  top: 60px;
  left: 0;
  bottom: 0;
  width: 85%;
  max-width: 300px;
  z-index: 100;
  box-shadow: 4px 0 20px rgba(0,0,0,0.15);
  border-right: none;
}
.close-btn {
  position: absolute;
  top: 12px;
  right: 12px;
  background: #ffe4ed;
  border: none;
  width: 32px;
  height: 32px;
  border-radius: 30px;
  font-size: 1.1rem;
  cursor: pointer;
  color: #db2777;
  display: flex;
  align-items: center;
  justify-content: center;
}
.profile {
  text-align: center;
  margin: 16px 0 24px 0;
  padding-bottom: 16px;
  border-bottom: 2px dashed #ffe0e7;
}
.avatar-icon {
  font-size: 48px;
  margin-bottom: 8px;
}
.profile h4 {
  font-weight: 700;
  color: #be185d;
}
.profile p {
  font-size: 0.7rem;
  color: #f472b6;
}
.nav {
  flex: 1;
  padding: 0 12px;
  display: flex;
  flex-direction: column;
  gap: 4px;
}
.nav-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 10px 16px;
  border-radius: 14px;
  font-weight: 500;
  color: #831843;
  cursor: pointer;
  transition: 0.2s;
}
.nav-item:hover {
  background: #fff0f5;
  color: #db2777;
}
.nav-item.active {
  background: #ffe4ed;
  color: #db2777;
  font-weight: 600;
}
.nav-icon {
  font-size: 1.2rem;
}
.footer {
  text-align: center;
  padding: 16px 0 12px 0;
  font-size: 0.7rem;
  color: #f9a8d4;
  border-top: 2px dashed #ffe0e7;
  margin-top: 16px;
}
/* Desktop: sembunyikan tombol close */
@media (min-width: 769px) {
  .close-btn {
    display: none;
  }
}
</style>