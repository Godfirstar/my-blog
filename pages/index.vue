<template>
  <div class="container">
    <h1>我的博客</h1>
    <div v-if="pending">加载中...</div>
    <div v-else class="post-list">
      <div v-for="post in posts" :key="post.id" class="post-item">
        <NuxtLink :to="`/post/${post.id}`">
          <h2>{{ post.title }}</h2>
          <p>{{ post.date }}</p>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>
// 使用 Nuxt 的 useFetch 或者 vue-notion 提供的组合式函数
import { getPageBlocks, getPageTable } from 'vue-notion'

// 假设这是你的 Notion Database ID
const NOTION_TABLE_ID = '2c77f6fa07148090b5fcfcde53ccbebb'

// 获取文章列表数据
const { data: posts, pending } = await useAsyncData('posts', async () => {
  // getPageTable 会把 Notion 的表格数据变成简单的 JSON 数组
  return await getPageTable(NOTION_TABLE_ID)
})
</script>