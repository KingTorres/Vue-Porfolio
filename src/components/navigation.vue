<script setup lang="ts">
import { useRouter } from 'vue-router';
const router = useRouter()
</script>
<template>
  <div>
    <button @click="router.push('/')">HOME</button>
    <button @click="router.push('/about')">ABOUT</button>
  </div>
</template>
<style scoped>
</style>
