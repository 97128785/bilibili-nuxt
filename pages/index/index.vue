<script setup lang="ts">
import type { VideoItem } from '@/types/video'
// 首次请求时，在服务端发送请求，浏览器就不会发送
// 通过 useFetch 获取频道列表数据，data是响应式数据

const { data: channelList } = await useFetch('/api/channel')
const { data: videoList } = await useFetch('/api/video')

// 显示的列表
const list = ref<VideoItem[]>([])
// 加载状态
const loading = ref(false)
// 是否加载完成
const finished = ref(false)

let page = 1
let pageSize = 20

// 滚动触底触发
const onLoad = () => {
  // 正在加载
  loading.value = true
  setTimeout(() => {
    // 根据当前页码提取数据
    let data = videoList.value?.slice((page - 1) * pageSize, page * pageSize) as VideoItem[]
    // 追加数据到渲染列表
    list.value.push(...data)
    // 加载完成
    loading.value = false
  }, 1000)

  // 页码累加
  page++

  // 加载结束
  if (videoList.value?.length === list.value.length) {
    finished.value = true
  }
}

// 初始化加载，主动请求前20条数据，用于首屏渲染，方便 SEO 抓取数据
onLoad()
</script>

<template>
  <AppHeader />
  <!-- 频道模块 -->
  <van-tabs>
    <van-tab v-for="item in channelList" :key="item.id" :title="item.name" />
  </van-tabs>
  <!-- 视频列表 -->
  <van-list
    v-model:loading="loading"
    :finished="finished"
    finished-text="没有更多了"
    @load="onLoad"
  >
    <div class="video-list">
      <AppVideo v-for="item in list" :key="item.aid" :item="item" />
    </div>
  </van-list>
</template>

<style lang="scss">
// 视频列表
.video-list {
  display: flex;
  flex-wrap: wrap;
  padding: 10px 5px;
}
</style>
