<template>
  <div class="article">
    <div v-if="pending">加载文章中...</div>
    <NotionRenderer v-else :block-map="blockMap" full-page prism />
  </div>
</template>

<script setup>
import { NotionRenderer, getPageBlocks } from 'vue-notion'
import 'vue-notion/dist/style.css' // 引入默认样式
import 'prismjs/themes/prism.css'  // 如果你有代码块，引入高亮样式

const route = useRoute()
const pageId = route.params.id

// 根据 URL 中的 ID 获取 Notion 页面的所有 Block
const { data: blockMap, pending } = await useAsyncData(`post-${pageId}`, async () => {
  return await getPageBlocks(pageId)
})
</script>