<script setup lang="ts">
import type { Post } from '@/models/post.model'
import { onMounted, ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const posts = ref<Post[]>([])

async function getPosts() {
  const result = await fetch('https://jsonplaceholder.typicode.com/posts')
  const data: Post[] = await result.json()

  posts.value = data
}

async function navigate(id: number) {
  await router.push({ name: 'post-detail', params: { id: id } })
}

onMounted(() => {
  getPosts()
})
</script>

<template>
  <main>
    <h1 class="title">Posts</h1>

    <ul>
      <li v-for="post in posts" :key="post.id" class="list-item">
        <div @click="navigate(post.id)">
          <h2>{{ post.title }}</h2>
          <p>{{ post.body }}</p>
        </div>
      </li>
    </ul>
  </main>
</template>
