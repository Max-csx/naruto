<script lang="ts" setup>
import { ref, watch } from 'vue'
import { RouterLink } from 'vue-router'
const selectedKeys = ref<string[]>([location.pathname])

defineProps<{ navMenus: Array<{ name: string; path: string; icon?: string }> }>()

watch(
  location.pathname,
  () => {
    if (selectedKeys.value[0] !== location.pathname) {
      selectedKeys.value = [location.pathname]
      console.log('路由变化:', location.pathname)
    }
  },
  { deep: true, immediate: true },
)
</script>

<template>
  <a-layout class="layout">
    <a-layout-header>
      <div class="logo" />
      <a-menu
        v-model:selectedKeys="selectedKeys"
        theme="dark"
        mode="horizontal"
        :style="{ lineHeight: '64px' }"
      >
        <a-menu-item
          v-for="navMenu in navMenus"
          :key="navMenu.path"
          :icon="navMenu.icon"
          :href="navMenu.path"
          ><RouterLink :to="{ path: navMenu.path }">{{ navMenu.name }}</RouterLink></a-menu-item
        >
      </a-menu>
    </a-layout-header>
    <a-layout-content style="padding: 0 50px">
      <div :style="{ background: '#fff', padding: '24px', minHeight: '280px' }"><slot /></div>
    </a-layout-content>
    <a-layout-footer style="text-align: center">
      Ant Design ©2018 Created by Ant UED
    </a-layout-footer>
  </a-layout>
</template>

<style scoped>
.layout {
  min-height: 100vh;
}

.site-layout-content {
  min-height: 280px;
  padding: 24px;
  background: #fff;
}
#components-layout-demo-top .logo {
  float: left;
  width: 120px;
  height: 31px;
  margin: 16px 24px 16px 0;
  background: rgba(255, 255, 255, 0.3);
}
.ant-row-rtl #components-layout-demo-top .logo {
  float: right;
  margin: 16px 0 16px 24px;
}

[data-theme='dark'] .site-layout-content {
  background: #141414;
}
</style>
