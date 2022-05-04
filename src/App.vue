<template>
  <n-config-provider :theme="apptheme">
    <n-message-provider>
      <router-view></router-view>
    </n-message-provider>
  </n-config-provider>
</template>
<script setup lang="ts">
import { title } from 'process';
import { useAppStore } from './store/modules/app'


import { ref, watch } from 'vue'
import { darkTheme } from 'naive-ui'
const appStore = useAppStore()
const apptheme = ref()

// provide('reload', reload)
// function reload() {
//   isRouterAlive.value = false
//   nextTick(() => (isRouterAlive.value = true))
// }

// const isRouterAlive = ref(true)

// watch(
//   () => appStore.title,
//   () => {
//     const title: string = appStore.title
//     document.title = title
//       ? `${title} - ${import.meta.env.VITE_APP_TITLE}`
//       : import.meta.env.VITE_APP_TITLE
//   },
//   {
//     immediate: true,
//   }
// )

watch(
  () => appStore.theme,
  () => {
    const theme: string = appStore.theme
    if (theme == "dark") {
      apptheme.value = darkTheme
    } else {
      apptheme.value = null
    }
  },
  {
    immediate: true,
  }
)
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: var(--color-bg-1);
  height: 100vh;
  overflow: hidden;
}
</style>
