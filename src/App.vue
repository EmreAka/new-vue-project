<script lang="ts" setup>
import { useRouter } from 'vue-router'

const router = useRouter()

const handleLogin = async () => {
  await router.push('login')
}
</script>

<template>
  <nav class="nav">
    <h1>Emre AKA</h1>
    <button class="btn-primary" @click="handleLogin">Login</button>
  </nav>
  <RouterView />
</template>
