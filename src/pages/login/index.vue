<script setup lang="ts">
import { reactive, ref } from 'vue'
import Header from '@/components/Header/index.vue'
import commuse from './components/commuse.vue'
import { useWebSocket } from '@vueuse/core'

var wss = ref('')

function login() {
  const { status, data, send, open, close } = useWebSocket(wss.value)
}
</script>
<template>
  <Header />
  <div class="cont">
    <div class="title">
      启用插件
      <a
        href="https://github.com/liujiaqi7998/GrasscuttersWebDashboard"
        target="_blank"
        rel="noopener noreferrer"
        >GrasscuttersWebDashboard</a
      >
    </div>
    <div>
      <div class="commuse-item">
        <div class="text-slate-900 dark:text-slate-100"> wss: </div>
        <n-input v-model:value="wss" clearable placeholder="请从控制台获取" />
      </div>
      <div class="title">
        <n-button type="tertiary" @click="login"> 登录 </n-button>
      </div>
    </div>
  </div>
</template>
<style lang="less" scoped>
.cont {
  width: 800px;
  margin: auto;
  margin-top: 40px;
  .title {
    text-align: center;
  }
  .commuse-item {
    display: flex;
    align-items: center;
    color: #000;
    margin: 18px 0;

    > div {
      &:nth-child(1) {
        width: 150px;
        text-align: right;
        padding-right: 10px;
      }
    }
  }
}
</style>