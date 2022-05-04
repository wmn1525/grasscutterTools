
<script setup lang="ts">
import { reactive, ref, computed } from 'vue'
import { useClipboard } from '@vueuse/core'
import { useMessage } from 'naive-ui'

import monster from './json/monster.json'
const { text, isSupported, copy } = useClipboard()



var value2 = ref(21010101)
var grade = ref(80)
var num = ref(10)

const value = computed(() => {
  return `/spawn ${value2.value} ${num.value} ${grade.value}`
})
const options = reactive(
  monster
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
 

    <div class="commuse-item">
      <div class="text-slate-900 dark:text-slate-100">
        怪物:
      </div>
      <n-select v-model:value="value2" filterable :options="options" />
    </div>
   <div class="commuse-item">
      <div class="text-slate-900 dark:text-slate-100">
        等级:
      </div>
      <n-input v-model:value="grade" type="text" placeholder="" />
    </div>
    <div class="commuse-item">
      <div class="text-slate-900 dark:text-slate-100">
        数量:
      </div>
      <n-input-number v-model:value="num" clearable />
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
