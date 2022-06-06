
<script setup lang="ts">
import { reactive, ref, computed } from 'vue'
import { useClipboard } from '@vueuse/core'
import { Message } from '@arco-design/web-vue'
import { useAppStore } from '@/store/modules/app'

const { text, isSupported, copy } = useClipboard()
const appStore = useAppStore()

const options = reactive([
  {
    title: '治疗队伍中所有角色',
    value: 'heal',
  },
  {
    title: '列出在线玩家',
    value: 'list',
  },
  {
    title: '获取当前坐标',
    value: 'position',
  },
  {
    title: '重载服务器配置',
    value: 'reload',
  },
  {
    title: '重启服务端',
    isuse: '均可使用',
    value: 'restart',
  },
  {
    title: '停止服务器',
    value: 'stop',
  },
  {
    title: '世界等级8',
    value: 'setworldlevel 8',
  },
])
const message = Message

function copyvalue(value: string) {
  copy(value)
  if (isSupported) {
    message.success(`已复制${value}`)
  }
}
const send: any = inject("send")
</script>

<template>
  <div class="commuse">
    <div v-for="(item, index) in options" :key="index">
      <div class="text-slate-900 dark:text-slate-100">{{ item.title }}</div>
      <div>
        <a-input v-model="item.value" placeholder="" disabled />
      </div>
      <div>
        <a-button type="outline" @click="copyvalue(item.value)">复制</a-button>
        <a-button type="outline" v-if="appStore.isLogin" @click="send(item.value)">执行</a-button>
      </div>
    </div>
  </div>
</template>
<style lang="less" scoped>
.commuse {
  width: 500px;
  margin: auto;

  >div {
    margin: 10px 0;
    display: flex;
    align-items: center;
    color: #000;

    >div {
      &:nth-child(1) {
        width: 130px;
      }

      margin: 0 5px;
    }
  }
}

.generate {
  display: flex;
  align-items: center;
  margin-left: 100px;
}
</style>
