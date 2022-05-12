<script setup lang="ts">
import { reactive, ref, watch } from 'vue'
import Header from '@/components/Header/index.vue'
import commuse from './components/commuse.vue'
import { Message } from '@arco-design/web-vue'
import { useAppStore, useUserStore } from '@/store'
const appStore = useAppStore()

var wss = ref('')
function login() {
  if (wss.value) {
    appStore.socketConnect(wss.value)
  } else {
    Message.error(`地址不正确`)
  }
}

function send() {
  const send_msg = {
    type: 'CMD',
    data: 'g',
  }
  const send_msg_str = JSON.stringify(send_msg)
  appStore.socketSend(send_msg_str)
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
        <a-input v-model="wss" clearable placeholder="请从控制台获取" />
      </div>
      <div class="title">
        <a-button type="outline" @click="login"> 登录 </a-button>
      </div>
    </div>
    <div>
      <a-button type="outline" @click="send"> send </a-button>
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