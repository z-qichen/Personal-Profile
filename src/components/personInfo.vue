<template>
    <div class="Info-wrapper">
        <div class="Info-container">
            <a href="tencent://message/?uin=2857498971" title="QQ: 2857498971" class="icon"
                @mouseenter="hovered = 'qq'" @mouseleave="hovered = ''">
                <i class="fa-brands fa-qq"></i>
            </a>
            <a href="javascript:void(0)" title="微信: 13037343312" class="icon"
                @mouseenter="hovered = 'wechat'" @mouseleave="hovered = ''">
                <i class="fa-brands fa-weixin"></i>
            </a>
            <a href="https://github.com/z-qichen" target="_blank" title="GitHub" class="icon"
                @mouseenter="hovered = 'github'" @mouseleave="hovered = ''">
                <i class="fa-brands fa-github"></i>
            </a>
            <a href="mailto:13037343312@163.com" title="邮箱: 13037343312@163.com" class="icon"
                @mouseenter="hovered = 'email'" @mouseleave="hovered = ''">
                <i class="fa-solid fa-envelope"></i>
            </a>
        </div>
        <div class="Info-text" :class="{ active: hovered }">{{ infoText }}</div>
    </div>
</template>
<script lang="ts" setup>
import { ref, computed } from 'vue'

const hovered = ref('')

const map: Record<string, string> = {
  qq: 'QQ：2857498971',
  wechat: '微信：13037343312',
  github: 'GitHub：z-qichen',
  email: '邮箱：13037343312@163.com',
}

const infoText = computed(() => map[hovered.value] || '')
</script>
<style lang="less" scoped>
.Info-wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.Info-container {
    height: 40px;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 12px;
    border-radius: 10px;
    transition: background-color 0.3s;

    &:hover {
        background-color: rgba(102, 105, 108, 0.5);
        transition: background-color 0.3s
    }
}

.Info-text {
    height: 40px;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 10px;
    color: #fff;
    font-size: 0.9rem;
    margin-top: 8px;
    background-color: transparent;
    transition: background-color 0.3s;
}

.Info-text.active {
    background-color: rgba(102, 105, 108, 0.5);
}

.icon {
    width: 31px;
    height: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 24px;
    color: #fff;
    transition: transform 0.3s;

    &:hover {
        transform: scale(1.3);
    }
}
</style>
