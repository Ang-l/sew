
<template>
  <view class="container pb-32">
    <!-- Header -->
    <view class="nav-bar">
      <text class="material-symbols-outlined back-btn" @tap="goBack">arrow_back_ios_new</text>
      <text class="title font-serif">美食分类</text>
    </view>

    <view class="px-5">
      <view class="category-grid">
        <view v-for="(cat, index) in categories" :key="cat.id" 
              class="cat-item editorial-shadow" 
              :class="{'full-width': index === 0 || index === 3}"
              @tap="goToList(cat)">
          <image :src="cat.image" mode="aspectFill" class="w-full h-full absolute inset-0" />
          <view class="overlay"></view>
          <view class="content">
            <text class="name" :class="{'large': index === 0 || index === 3}">{{cat.name}}</text>
            <text class="subtitle">{{cat.subtitle}}</text>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
import { CATEGORIES } from '../../common/constants';

export default {
  data() {
    return {
      categories: CATEGORIES
    }
  },
  methods: {
    goBack() { uni.navigateBack(); },
    goToList(cat) {
      uni.navigateTo({ url: `/pages/recipe-list/index?catId=${cat.id}` });
    }
  }
}
</script>

<style scoped>
.nav-bar { display: flex; align-items: center; padding: 60rpx 40rpx 40rpx; background: #f5f3f0; position: sticky; top: 0; z-index: 50; }
.back-btn { font-size: 40rpx; color: #379587; }
.title { flex: 1; text-align: center; font-size: 34rpx; font-weight: bold; margin-right: 40rpx; }

.category-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 30rpx; margin-top: 20rpx; }
.cat-item { position: relative; border-radius: 50rpx; overflow: hidden; background: #eee; aspect-ratio: 1/1; }
.cat-item.full-width { grid-column: span 2; aspect-ratio: 16/8; }

.overlay { position: absolute; inset: 0; background: linear-gradient(to top, rgba(0,0,0,0.7), rgba(0,0,0,0.1)); }
.content { position: absolute; bottom: 0; left: 0; padding: 40rpx; width: 100%; box-sizing: border-box; }
.name { color: white; font-weight: bold; font-size: 36rpx; display: block; }
.name.large { font-size: 56rpx; }
.subtitle { color: rgba(255,255,255,0.8); font-size: 20rpx; text-transform: uppercase; letter-spacing: 4rpx; margin-top: 10rpx; display: block; }
</style>
