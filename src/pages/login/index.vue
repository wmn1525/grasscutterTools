<script setup lang="ts">
import { reactive, ref, watch, onMounted } from 'vue'
import Header from '@/components/Header/index.vue'
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

function close() {
  appStore.socketClose()
}

function send() {
  const send_msg = {
    type: 'CMD',
    data: 'g',
  }
  const send_msg_str = JSON.stringify(send_msg)
  appStore.socketSend(send_msg_str)
}
const data = ref([
  {
    label: '系统运行时长',
    value: '14小时8分钟44秒',
  },
  {
    label: '在线玩家数量',
    value: '0',
  },
  {
    label: 'Tick耗时',
    value: '999',
  },
  {
    label: '内存占用',
    value: '66719376/101498880',
  }
])
const data2 = ref([
  {
    label: '服务器名称',
    value: 'ttt',
  },
  {
    label: '系统',
    value: 'win10',
  },
  {
    label: '服务器地址',
    value: '0.0.0.0',
  },
  {
    label: 'JAVA版本',
    value: '17.0',
  },
  {
    label: '插件版本',
    value: '1.0',
  }
])

onMounted(() => {
  const WSS = localStorage.getItem("WSS")
  if (WSS) {
    wss.value = WSS
  }
})

watch(
  () => appStore.tick,
  () => {
    data.value = appStore.tick
  },
  {
    immediate: true,
  },
)

watch(
  () => appStore.baseData,
  () => {
    data2.value = appStore.baseData
  },
  {
    immediate: true,
  },
)

</script>
<template>
  <div class="login" v-if="!appStore.isLogin">
    <div class="title text-slate-900 dark:text-slate-100">
      启用插件
      <!-- <a href="https://github.com/liujiaqi7998/GrasscuttersWebDashboard" target="_blank"
        rel="noopener noreferrer">GrasscuttersWebDashboard</a> -->
      <a-link href="https://github.com/liujiaqi7998/GrasscuttersWebDashboard" target="_blank" icon>
        GrasscuttersWebDashboard</a-link>
    </div>
    <div class="title text-slate-900 dark:text-slate-100">
      连接失败先去直接先https://ip
      访问一下 然后 高级 继续访问
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
  </div>
  <div v-else>
    <div class="inf">
      <a-descriptions style="margin-top: 20px" :data="data" size="large" title="运行状态" :column="1" />
      <a-descriptions style="margin-top: 20px" :data="data2" size="large" title="系统信息  " :column="1" />

    </div>
    <div>
      <a-button type="outline" @click="close"> 退出 </a-button>
    </div>
  </div>
</template>
<style lang="less" scoped>
.login {
  width: 600px;
  margin-top: 10vh;

  .title {
    text-align: center;
    line-height: 40px;
  }
  .commuse-item {
    display: flex;
    align-items: center;
    color: #000;
    margin: 18px 0;

    >div {
      &:nth-child(1) {
        width: 150px;
        text-align: right;
        padding-right: 10px;
      }
    }
  }
}
</style>