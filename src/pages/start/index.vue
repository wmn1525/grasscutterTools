<script setup lang="ts">
import { reactive, ref } from 'vue'
import Header from '@/components/Header/index.vue'
import startnav from './components/startnav.vue'
import commuse from './components/commuse.vue'


</script>
<template>
  <Header />
  <div class="cont">
    <startnav />
    <div class="selectcom">
      <commuse />
    </div>
  </div>

</template>
<style lang="less">
.cont {
  width: 1366px;
  margin: auto;
  display: flex;

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

  .selectcom {
    width: 1000px;
  }

}
</style>
