<script setup lang="ts">
// 使用 Nuxt 的 useSeoMeta 设置页面的 SEO 信息
useSeoMeta({
  // 网站标题
  title: '哔哩哔哩 (゜-゜)つロ 干杯~-bilibili',
  // 网站描述
  description:
    'bilibili是国内知名的在线视频弹幕网站，拥有最棒的ACG氛围，哔哩哔哩内容丰富多元，涵盖动漫、电影、二次元舞蹈视频、在线音乐、娱乐时尚、科技生活、鬼畜视频等。下载客户端还可离线下载电影、动漫。',
  // 搜索关键词
  keywords: 'B站,bilibili,哔哩哔哩,哔哩哔哩动画,动漫,电影,在线动漫,高清电影',
  // 绕开 B站图片防盗链
  referrer: 'no-referrer',
})
</script>

<template>
  <!-- Nuxt 页面路由，相当于 RouterView -->
  <!-- 缓存 10 级页面，提升用户切换体验 -->
  <NuxtPage :keepalive="{ max: 10 }" />
</template>

<style lang="scss">
// 全局导入样式
@import './assets/styles/base.scss';
// 字体图标
@import './assets/styles/iconfont.scss';

:root {
  /* CSS 变量设置组件库的主题色 */
  --van-primary-color: #fb7299 !important;
  --van-back-top-background: #fbfbfb !important;
  --van-back-top-text-color: #666 !important;
}
</style>
