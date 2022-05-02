
<script setup lang="ts">
import { reactive, ref, computed } from 'vue'
import { useClipboard } from '@vueuse/core'
import { useMessage } from 'naive-ui'
import holyrelicname from './json/holyrelicname.json'
import holyrelicnmain from './json/holyrelicnmain.json'
import holyrelicx from './json/holyrelicnx.json'
const { text, isSupported, copy } = useClipboard()




var uid = ref("")
var holyrelicnamevalue = ref("")
var holyrelicnmainvalue = ref("")

var grade = ref("0")
var selectedValue = ref()
var num = ref()

const value = computed(() => {

  var xct = ''
  options3.value.forEach(k => {
    if (k.isCheck) {
      xct = xct + ` ${k.value},${k.num}`
    }
  });
  return `/giveart ${uid.value} ${holyrelicnamevalue.value} ${holyrelicnmainvalue.value}${xct} ${grade.value + 1}`
})
const options = reactive(
  holyrelicname
)

const options2 = reactive(
  holyrelicnmain
)

var holyrelicx1 = holyrelicx.map(k => {
  const obj = {
    isCheck: false,
    num: 1,
    label: k.label,
    value: k.value
  }
  return obj
})
const options3 = ref(
  holyrelicx1
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
        圣遗物:
      </div>
      <n-select v-model:value="holyrelicnamevalue" filterable placeholder="选择圣遗物" :options="options" />
    </div>

    <div class="commuse-item">
      <div>
        主属性:
      </div>
      <n-select v-model:value="holyrelicnmainvalue" filterable placeholder="选择圣遗物主属性" :options="options2" />
    </div>

    <div class="commuse-item">
      <div>
        属性小词条:
      </div>
      <div class="smallho">
        <div v-for="(item, index) in options3" :key="index">
          <n-checkbox v-model:checked="item.isCheck" style="margin-right: 12px" />
          <div>{{ item.label }} </div>
          <div>
            <n-input-number v-model:value="item.num" :min="1" placeholder="" :show-button="false"/>
          </div>
        </div>

      </div>
    </div>

    <div class="commuse-item">
      <div>
        强化等级:
      </div>
      <n-input-number v-model:value="grade" placeholder="" :min="0" :max="20" :show-button="false"/>
    </div>

    <div class="generate">
      <n-input id="input" v-model:value="value" type="text" placeholder="" />
      <n-button type="tertiary" @click="copyvalue">
        复制
      </n-button>
    </div>
  </div>

</template>
<style lang="less">
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

.smallho {
  height: 300px;
  width: 100%;
  overflow: auto;

  >div {
    display: flex;
    justify-content: space-between;

    >div {
      &:nth-child(3) {
        width: 80px;
      }
    }
  }
}
</style>
