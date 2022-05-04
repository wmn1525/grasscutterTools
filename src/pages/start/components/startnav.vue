<script setup lang="ts">
import { reactive, ref } from 'vue'

const datav = reactive([
  { name: '常用', path: "/start/commuse" },
  { name: '圣遗物', path: "/start/holyrelic" },
  { name: '怪物生成', path: "/start/monster" },
  { name: '其它', path: "/start/other" },
  { name: '武器', path: "/start/weapon" },
  { name: '物品', path: "/start/thing" },
  { name: '角色属性', path: "/start/role" },
])

</script>
<template>
  <div class="nav ">
    <div v-for="(item, index) in datav" :key="index">
      <router-link :to="item.path" class="mr-3 flex-none w-[2.0625rem] md:w-auto leading-6 dark:text-slate-200">
        {{ item.name }}
      </router-link>
    </div>
  </div>
</template>
<style lang="less" scoped>
.nav {
  height: 600px;
  width: 120px;
  border-right: 1px solid #d1d1cb;
  padding-right: 30px;

  >div {
    margin: 10px 0;
    cursor: pointer;
    font-size: 18px;
    color: #000;
  }

}
</style>
