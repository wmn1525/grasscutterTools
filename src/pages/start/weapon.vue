<script setup lang="ts">
import { reactive, ref } from 'vue'
import Header from '@/components/Header/index.vue'
import startnav from './components/startnav.vue'
import holyrelic from './components/holyrelic.vue'


</script>
<template>
  <Header />
  <div class="cont">
    <startnav />
    <div class="selectcom">
      <h1>未开发</h1>

    </div>
  </div>

</template>
<style lang="less">
.cont {
  width: 1366px;
  margin: auto;
  display: flex;

  .selectcom {
    width: 1000px;
  }
}
</style>
