<template>
  <div class="home">
    <div class="welcome">
      <div>
        <h1>Halo, Fika 💗</h1>
        <p>Semangat belajar hari ini! Jangan lupa tersenyum ❤️</p>
      </div>
      <div class="date">{{ formattedDate }}</div>
    </div>
    <div class="stats">
      <div class="card">
        <div class="card-icon pink">📚</div>
        <div><div class="number">3</div><div class="label">Sesi belajar hari ini</div></div>
      </div>
      <div class="card">
        <div class="card-icon pink">✅</div>
        <div><div class="number">12/15</div><div class="label">Tugas semester</div></div>
      </div>
      <div class="card">
        <div class="card-icon pink">⏱️</div>
        <div><div class="number">24 jam</div><div class="label">Total belajar</div></div>
      </div>
    </div>
    <div class="agenda">
      <h3>📌 Agenda Hari Ini</h3>
      <div class="task" v-for="t in agenda" :key="t.time">
        <div class="time">{{ t.time }}</div>
        <div class="name">{{ t.name }}</div>
        <div class="emoji">{{ t.emoji }}</div>
      </div>
    </div>
  </div>
</template>

<script setup>
const formattedDate = new Date().toLocaleDateString('id-ID', { weekday: 'long', day: 'numeric', month: 'short' })
const agenda = [
  { time: '10:00', name: 'Matematika - Integral', emoji: '📐' },
  { time: '13:00', name: 'Vue.js - Komponen & Props', emoji: '💻' },
  { time: '15:30', name: 'Reading TOEFL Practice', emoji: '📖' }
]
</script>

<style scoped>
.home { max-width: 1200px; margin: 0 auto; }
.welcome { display: flex; justify-content: space-between; align-items: center; margin-bottom: 28px; flex-wrap: wrap; gap: 10px; }
.welcome h1 { font-size: 1.6rem; font-weight: 700; color: #be185d; }
.welcome p { color: #f472b6; }
.date { background: white; padding: 5px 16px; border-radius: 40px; border: 1px solid #ffe0e7; color: #db2777; font-size: 0.9rem; }
.stats { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 16px; margin-bottom: 32px; }
.card { background: white; border-radius: 24px; padding: 16px; display: flex; align-items: center; gap: 14px; border: 1px solid #ffe0e7; box-shadow: 0 2px 8px rgba(219,39,119,0.05); }
.card-icon { font-size: 2rem; padding: 8px; border-radius: 18px; }
.pink { background: #fff0f5; }
.number { font-size: 1.5rem; font-weight: 800; color: #be185d; }
.label { font-size: 0.75rem; color: #f472b6; }
.agenda { background: white; border-radius: 28px; padding: 20px; border: 1px solid #ffe0e7; }
.agenda h3 { margin-bottom: 16px; font-size: 1.1rem; color: #be185d; }
.task { display: flex; align-items: center; gap: 16px; padding: 10px 0; border-bottom: 1px solid #ffe0e7; }
.time { background: #fff0f5; padding: 3px 12px; border-radius: 40px; font-size: 0.7rem; font-weight: 600; color: #db2777; width: 70px; text-align: center; }
.name { flex: 1; font-weight: 500; color: #4a044e; font-size: 0.9rem; }
@media (max-width: 500px) {
  .welcome h1 { font-size: 1.3rem; }
  .number { font-size: 1.2rem; }
  .task .time { width: 60px; font-size: 0.65rem; }
}
</style>