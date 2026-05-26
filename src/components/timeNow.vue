<template>
  <div class="TimeCard">
    <div class="title">
      <h3>当前时间</h3>
    </div>
    <div class="time">{{ time }}</div>
    <div class="weather"></div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const time = ref(formatTime(new Date()))
let timer: number

onMounted(() => {
  const delay = 1000 - new Date().getMilliseconds()
  setTimeout(() => {
    time.value = formatTime(new Date())
    timer = window.setInterval(() => {
      time.value = formatTime(new Date())
    }, 1000)
  }, delay)
})

onUnmounted(() => clearInterval(timer))

function formatTime(d: Date) {
  return d.toLocaleTimeString('zh-CN', { hour12: false })
}
</script>

<style lang="less" scoped>
.TimeCard {
  background-color: rgba(102, 105, 108, 0.5);
  width: 351px;
  height: 207px;
  border-radius: 10px;
  padding: 30px;
  transition: transform 0.3s, background-color 0.3s;

  &:hover {
    transform: scale(1.05);
    background-color: rgba(102, 105, 108, 0.7);
  }
}

.title h3 {
  height: 50px;
  color: rgb(253, 253, 253);
  text-align: center;
}

.time {
  font-size: medium;
  text-align: center;
  color: rgb(253, 253, 253);
}
</style>