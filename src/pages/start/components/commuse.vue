
<script setup lang="ts">
import { reactive, ref, computed } from 'vue'
import { useClipboard } from '@vueuse/core'
import { useMessage } from 'naive-ui'

const { text, isSupported, copy } = useClipboard()

var value2 = ref(223)
var uid = ref('')
var num = ref(1000)

const value = computed(() => {
  return `/give ${uid.value} ${value2.value} ${num.value}`
})
const options = reactive([
  {
    label: '角色经验',
    value: 101,
  },
  {
    label: '冒险阅历',
    value: 102,
  },
  {
    label: '原石',
    value: 201,
  },
  {
    label: '摩拉',
    value: 202,
  },
  {
    label: '创世结晶',
    value: 203,
  },
  {
    label: '洞天宝钱',
    value: 204,
  },
  {
    label: '无主的星辉',
    value: 221,
  },
  {
    label: '无主的星尘',
    value: 222,
  },
  {
    label: '纠缠之缘',
    value: 223,
  },
  {
    label: '相遇之缘',
    value: 224,
  },
])
const message = useMessage()
function copyvalue() {
  copy(value.value)
  if (isSupported) {
    message.success(`已复制${value.value}`)
  }
}
</script>

<template>
  <div class="commuse">
    <div class="commuse-item">
      <div class="text-slate-900 dark:text-slate-100"> UID: </div>
      <a-input v-model="uid" placeholder="请输入UID" allow-clear />
    </div>

    <div class="commuse-item">
      <div class="text-slate-900 dark:text-slate-100"> 物品: </div>
      <a-cascader
        allow-search
        v-model="value2"
        :options="options"
        placeholder="请输入物品"
        filterable
      />
    </div>

    <div class="commuse-item">
      <div class="text-slate-900 dark:text-slate-100"> 数量: </div>
      <a-input-number
        v-model="num"
        placeholder="请输入数量"
        mode="button"
        size="large"
        class="input-demo"
      />
    </div>
    <div class="generate">
      <a-input v-model="value" placeholder="请输入UID" />
      <a-button type="outline" @click="copyvalue">复制</a-button>
      <!-- <a-button type="outline" @click="copyvalue">执行</a-button> -->
    </div>
  </div>

  <div> </div>
</template>
<style lang="less" scoped>
.commuse {
  width: 500px;
  margin: auto;
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

.generate {
  display: flex;
  align-items: center;
  margin-left: 100px;
}
</style>
