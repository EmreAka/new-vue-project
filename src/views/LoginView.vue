<script lang="ts" setup>
import { computed, reactive, watchEffect } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const form = reactive({
  email: '',
  password: ''
})

const greeting = computed(() => `Hi ${form.email}`)

const handleLogin = async () => {
  await router.push({ name: 'home' })
}

watchEffect(() => {
  console.log(form.email)
})
</script>

<template>
  <main>
    <h1 class="title">Login</h1>

    <p class="text" v-if="form.email != ''">{{ greeting }}</p>

    <form class="form" @submit.prevent="handleLogin">
      <label for="email" class="label">Email</label>
      <input type="email" id="email" class="input" v-model="form.email" />

      <label for="password" class="label">Password</label>
      <input type="password" id="password" class="input" v-model="form.password" />

      <button class="btn-secondary" type="submit">Login</button>
    </form>
  </main>
</template>
