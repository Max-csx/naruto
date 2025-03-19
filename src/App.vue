<script setup lang="ts">
import { RouterView } from 'vue-router'
import AppLayout from './layout/AppLayout.vue'

const navMenus = [
  {
    name: 'Home',
    path: '/',
  },
  {
    name: 'About',
    path: '/about',
  },
]
</script>

<template>
  <AppLayout :navMenus="navMenus">
    <RouterView />
  </AppLayout>
</template>

<style scoped></style>
