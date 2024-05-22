<script setup lang="ts">
import type { Post } from '@/models/post.model'
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()

const post = ref<Post | undefined>(undefined)

async function getPost() {
  const postId = route.params.id
  const result = await fetch('https://jsonplaceholder.typicode.com/posts/' + postId)
  const data: Post = await result.json()

  post.value = data
}

onMounted(() => {
  getPost()
})
</script>

<template>
  <main>
    <h1 class="title">Posts</h1>

    <ul>
      <li v-if="post" class="list-item">
        <div>
          <h2>{{ post.title }}</h2>
          <p>{{ post.body }}</p>
        </div>
      </li>
    </ul>
  </main>
</template>
