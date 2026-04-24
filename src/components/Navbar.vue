<script setup>
defineProps({ isMobile: Boolean })
const emit = defineEmits(['toggleSidebar'])
</script>

<template>
  <header class="navbar">
    <div class="left">
      <button v-if="isMobile" class="hamburger" @click="emit('toggleSidebar')">☰</button>
      <div class="brand">
        <span class="logo">📖💗</span>
        <span class="title">StudyPlanner</span>
      </div>
    </div>
    <div class="user">
      <span class="name">Fika</span>
      <span class="avatar">🌸</span>
    </div>
  </header>
</template>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
  height: 60px;
  background: white;
  border-bottom: 2px solid #ffe0e7;
  box-shadow: 0 2px 6px rgba(219,39,119,0.05);
}
.left {
  display: flex;
  align-items: center;
  gap: 12px;
}
.hamburger {
  background: #ffe4ed;
  border: none;
  font-size: 1.5rem;
  width: 40px;
  height: 40px;
  border-radius: 12px;
  cursor: pointer;
  color: #db2777;
  display: flex;
  align-items: center;
  justify-content: center;
}
.brand {
  display: flex;
  align-items: baseline;
  gap: 6px;
}
.logo { font-size: 1.4rem; }
.title {
  font-weight: 700;
  font-size: 1.2rem;
  background: linear-gradient(120deg, #db2777, #f472b6);
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
}
.user {
  display: flex;
  align-items: center;
  gap: 6px;
  background: #fff0f5;
  padding: 4px 12px 4px 16px;
  border-radius: 40px;
  border: 1px solid #ffe0e7;
}
.name { font-weight: 600; font-size: 0.85rem; color: #be185d; }
.avatar { font-size: 1rem; }
@media (max-width: 480px) {
  .navbar { padding: 0 12px; }
  .title { font-size: 1rem; }
  .name { display: none; }
  .user { padding: 4px 8px; }
}
</style>