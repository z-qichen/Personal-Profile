<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import backGround from './components/backGround.vue'
import smallCard from './components/smallCard.vue'
import personInfo from './components/personInfo.vue'

const dateStr = ref('')
const timeStr = ref('')
const quote = ref('')
const quoteFrom = ref('')
let timer: number

async function fetchQuote() {
  try {
    const res = await fetch('https://v1.hitokoto.cn/')
    const data = await res.json()
    quote.value = data.hitokoto
    quoteFrom.value = data.from
  } catch {
    quote.value = '生活不止眼前的苟且，还有诗和远方的田野。'
    quoteFrom.value = '高晓松'
  }
}

function tick() {
  const d = new Date()
  dateStr.value = d.toLocaleDateString('zh-CN', {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
    weekday: 'long',
  })
  timeStr.value = d.toLocaleTimeString('zh-CN', { hour12: false })
}

onMounted(() => {
  tick()
  timer = window.setInterval(tick, 1000)
  fetchQuote()
})

onUnmounted(() => clearInterval(timer))
</script>

<template>
  <backGround />
  <div class="layout">
    <!-- 左上：圆形时钟 Logo + 站点名 -->
    <div class="logo-area glass">
      <div class="clock-logo">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
          <circle cx="12" cy="12" r="10" />
          <path d="M12 6v6l4 2" />
        </svg>
      </div>
      <span class="site-name">imsyy.top</span>
    </div>

    <!-- 右上左：每日一言 -->
    <div class="quote-card glass">
      <p class="quote-text">"{{ quote }}"</p>
      <p class="quote-author">—— {{ quoteFrom }}</p>
    </div>

    <!-- 右上右：时间卡片 -->
    <div class="time-card glass">
      <p class="date-text">{{ dateStr }}</p>
      <p class="time-text">{{ timeStr }}</p>
      <p class="weather-text">☀️ 晴 25°C</p>
    </div>

    <!-- 中左：欢迎语大卡片 -->
    <div class="welcome-card glass">
      <p class="welcome-text">"低代码平台 — 可视化拖拽搭建页面，快速构建应用。"</p>
      <p class="welcome-text">mini-vue — 从零实现的精简版 Vue 框架，深入响应式原理。"</p>
    </div>

    <!-- 中右：链接 + 站点监测 -->
    <div class="links-stack">
      <smallCard icon="🔗" text="低代码平台" href="https://vue-dima.vercel.app/" />
      <smallCard icon="🖥️" text="mini-vue" href="https://my-minivue.vercel.app/" />
    </div>

    <!-- 左下：社交图标 -->
    <personInfo class="social-area" />

  </div>
</template>

<style scoped>
.layout {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 20px;
  max-width: 1200px;
  margin: 0 auto;
  padding: 40px;
  min-height: 100vh;
  position: relative;
  z-index: 1;
  align-content: center;
}

/* 通用玻璃拟态卡片 */
.glass {
  background: rgba(0, 0, 0, 0.15);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  color: #fff;
  padding: 24px;
  transition: transform 0.3s, background 0.3s;
}

.glass:hover {
  transform: scale(1.04);
  background: rgba(0, 0, 0, 0.25);
}

/* 左上：Logo 区域 */
.logo-area {
  grid-column: 1;
  grid-row: 1;
  display: flex;
  align-items: center;
  gap: 12px;
}

.clock-logo {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.15);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.clock-logo svg {
  width: 28px;
  height: 28px;
  color: #fff;
}

.site-name {
  font-family: 'Segoe Script', 'Comic Sans MS', cursive;
  font-size: 1.4rem;
  color: #fff;
  white-space: nowrap;
}

/* 每日一言卡片 */
.quote-card {
  grid-column: 2;
  grid-row: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.quote-text {
  font-size: 0.95rem;
  line-height: 1.6;
  font-style: italic;
}

.quote-author {
  margin-top: 8px;
  text-align: right;
  font-size: 0.85rem;
  opacity: 0.7;
}

/* 时间卡片 */
.time-card {
  grid-column: 3;
  grid-row: 1;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.date-text {
  font-size: 0.9rem;
  opacity: 0.8;
  margin-bottom: 8px;
}

.time-text {
  font-size: 2.8rem;
  font-family: 'Courier New', 'Consolas', monospace;
  font-weight: bold;
  letter-spacing: 2px;
  font-variant-numeric: tabular-nums;
}

.weather-text {
  margin-top: 8px;
  font-size: 0.9rem;
  opacity: 0.8;
}

/* 欢迎语大卡片 */
.welcome-card {
  grid-column: 1 / 3;
  grid-row: 2;
  padding: 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-height: 140px;
}

.welcome-text {
  font-size: 1.3rem;
  line-height: 1.8;
  font-style: italic;
}

/* 链接堆叠区 */
.links-stack {
  grid-column: 3;
  grid-row: 2;
  display: flex;
  flex-direction: column;
  gap: 16px;
  align-items: center;
  justify-content: center;
}

/* 社交图标区 */
.social-area {
  grid-column: 1;
  grid-row: 3;
  align-self: center;
}

/* 头像区 */
.avatars-area {
  grid-column: 3;
  grid-row: 3;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 12px;
}

.avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.15);
  border: 2px solid rgba(255, 255, 255, 0.2);
  transition: transform 0.3s;
  cursor: pointer;
}

.avatar:hover {
  transform: scale(1.15);
}


/* ========== 响应式 ========== */
@media (max-width: 900px) {
  .layout {
    grid-template-columns: 1fr 1fr;
    padding: 24px;
    align-content: start;
  }

  .logo-area    { grid-column: 1; grid-row: 1; }
  .quote-card   { grid-column: 2; grid-row: 1; }
  .time-card    { grid-column: 1 / -1; grid-row: 2; }
  .welcome-card { grid-column: 1 / -1; grid-row: 3; }
  .links-stack  { grid-column: 1 / -1; grid-row: 4; flex-direction: row; }
  .social-area  { grid-column: 1; grid-row: 5; }
  .avatars-area { grid-column: 2; grid-row: 5; justify-content: flex-end; }
  .indicator    { grid-row: 6; }
  .footer       { grid-row: 7; }

  .time-text { font-size: 2.2rem; }
}

@media (max-width: 600px) {
  .layout {
    grid-template-columns: 1fr;
  }

  .logo-area,
  .quote-card,
  .time-card,
  .welcome-card,
  .links-stack,
  .social-area,
  .avatars-area {
    grid-column: 1;
  }

  .logo-area    { grid-row: 1; }
  .quote-card   { grid-row: 2; }
  .time-card    { grid-row: 3; }
  .welcome-card { grid-row: 4; }
  .links-stack  { grid-row: 5; flex-direction: column; align-items: center; }
  .social-area  { grid-row: 6; }
  .avatars-area { grid-row: 7; justify-content: center; }
  .indicator    { grid-row: 8; }
  .footer       { grid-row: 9; }

  .time-text  { font-size: 2rem; }
  .welcome-card { padding: 24px; }
  .welcome-text { font-size: 1.1rem; }
}
</style>
