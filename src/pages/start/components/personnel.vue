<template>
  <div class="personnel">
    <a-table :columns="columns" :data="data">
      <template #optional="{ record }">
        <a-button @click="$modal.info({ title: 'Name', content: record.name })">操作</a-button>
      </template>
    </a-table>
  </div>
</template>
<script setup lang="ts">
import { reactive, ref, computed } from 'vue'

const data = ref([])
const columns = [
  {
    title: 'UID',
    dataIndex: 'uid',
  },
  {
    title: '昵称',
    dataIndex: 'nickname',
  },
  {
    title: '签名',
    dataIndex: 'signature',
  },
  {
    title: '等级',
    dataIndex: 'Level',
  },
  {
    title: '坐标',
    dataIndex: 'pos',
  },
  {
    title: '场景',
    dataIndex: 'SceneId',
  },
  {
    title: '操作',
    dataIndex: 'Optional',
  },
];
</script>
<style lang="less" scoped>
.personnel {
  margin-top: 20px;
  width: 700px;
}
</style>

