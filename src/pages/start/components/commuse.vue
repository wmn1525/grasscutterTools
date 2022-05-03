
<script setup lang="ts">
import { reactive, ref, computed } from 'vue'
import { useClipboard } from '@vueuse/core'
import { useMessage } from 'naive-ui'
const { text, isSupported, copy } = useClipboard()




var value2 = ref(223)
var uid = ref("")
var num = ref(1000)

const value = computed(() => {
  return `/give ${uid.value} ${value2.value} ${num.value}`
})
const options = reactive(
  [
    {
      "label": "角色经验",
      "value": 101
    },
    {
      "label": "冒险阅历",
      "value": 102
    },
    {
      label: "原石",
      value: 201,
    },
    {
      label: "摩拉",
      value: 202,
    },
    {
      label: "创世结晶",
      value: 203,
    },
    {
      label: "洞天宝钱",
      value: 204,
    },
    {
      label: "无主的星辉",
      value: 221,
    },
    {
      label: "无主的星尘",
      value: 222,
    },
    {
      label: "纠缠之缘",
      value: 223,
    },
    {
      label: "相遇之缘",
      value: 224,
    }
  ]
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
      <div>
        UID:
      </div>
      <n-input v-model:value="uid" type="text" placeholder="" />
    </div>

    <div class="commuse-item">
      <div>
        物品:
      </div>
      <n-select filterable v-model:value="value2" :options="options" />
    </div>

    <div class="commuse-item">
      <div>
        数量:
      </div>
      <n-input-number  v-model:value="num" clearable />
    </div>
    <div class="generate">
      <n-input id="input" v-model:value="value" type="text" placeholder="" />
      <n-button type="tertiary" @click="copyvalue">
        复制
      </n-button>
    </div>

    
  </div>

  <div>
    
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
