
<script setup lang="ts">
import { reactive, ref, computed } from 'vue'
import { useClipboard } from '@vueuse/core'
import { useMessage } from 'naive-ui'

import role from './json/role.json'

const { text, isSupported, copy } = useClipboard()




var value2 = ref()
var num = ref()

const value = computed(() => {
  return `/setstats ${value2.value} ${num.value}`
})
const options = reactive(
  role
)
const message = useMessage()

function copyvalue() {
  copy(value.value)
  if (isSupported) {
    message.success(
      `已复制${value.value}`
    )
  }

}


</script>

<template>

  <div class="commuse">
    <div class="title">
      直接修改当前角色的面板
    </div>
    <div class="commuse-item">
      <div>
        属性:
      </div>
      <n-select v-model:value="value2" :options="options" placeholder=""/>
    </div>

    <div class="commuse-item">
      <div>
        数值:
      </div>
       <n-input v-model:value="num" type="text" placeholder="" />
    </div>
    <div class="generate">
      <n-input id="input" v-model:value="value" type="text" placeholder="" />
      <n-button type="tertiary" @click="copyvalue">
        复制
      </n-button>
    </div>
  </div>

</template>
<style lang="less" scoped>
.commuse {
  width: 500px;
  margin: auto;
}

.title {
  text-align: center;
  font-size: 16px;
  margin: 10px 0;
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

.generate {
  display: flex;
  align-items: center;
  margin-left: 100px;
}
</style>
