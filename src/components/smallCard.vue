<script setup lang="ts">
defineProps<{
  icon?: string
  text?: string
  href?: string
}>()
</script>

<template>
<a v-if="href" :href="href" target="_blank" class="boxCard">
    <div class="icon">{{ icon }}</div>
    <div class="text">{{ text }}</div>
</a>
<div v-else class="boxCard">
    <div class="icon">{{ icon }}</div>
    <div class="text">{{ text }}</div>
</div>
</template>

<style lang="less" scoped>
.boxCard{
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 12px;
    background: rgba(0, 0, 0, 0.15);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    width: 225px;
    height: 126px;
    border-radius: 16px;
    transition: transform 0.3s;

    &:hover {
      transform: scale(1.05);
      background: rgba(0, 0, 0, 0.25);
    }
}


.icon{
    color: rgb(253, 253, 253);
}
.text{
    font-size: medium;
    color: rgb(253, 253, 253);
}
</style>