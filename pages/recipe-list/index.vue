
<template>
  <view class="list-container">
    <view class="nav-bar">
      <view class="status-bar"></view>
      <view class="nav-content">
        <view class="back-btn" @tap="goBack">
          <text class="material-symbols-outlined">arrow_back_ios_new</text>
        </view>
        <!-- <text class="nav-title">{{category.name}}精选</text> -->
        <!-- <view class="placeholder"></view> -->
      </view>
    </view>

    <!-- 顶部大标题 -->
    <view class="list-header">
      <text class="header-sub">Simply Eat Well</text>
      <text class="header-main">{{category.name}} · 灵感辑</text>
    </view>

    <!-- 菜谱网格 -->
    <view class="recipe-grid">
      <view v-for="(r, index) in recipes" :key="r.id" 
            class="recipe-card" 
            :class="{'full-card': index === 0}"
            @tap="goToDetail(r)">
        <view class="img-wrap">
          <image :src="r.image" mode="aspectFill" class="card-img" />
          <view class="card-badge" v-if="index === 0">RECOMMENDED</view>
          <view class="card-info-overlay">
             <text class="card-time">{{r.prepTime}}</text>
             <text class="card-difficulty">{{r.difficulty}}</text>
          </view>
        </view>
        <view class="card-body">
          <text class="card-name">{{r.name}}</text>
          <text class="card-tagline">“ {{r.tagline}} ”</text>
          <view class="card-footer">
            <text class="footer-link">查看详情</text>
            <text class="material-symbols-outlined footer-icon">arrow_forward</text>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
import { CATEGORIES, RECIPES } from '../../common/constants';

export default {
  data() {
    return {
      category: {},
      recipes: []
    }
  },
  onLoad(options) {
    const catId = options.catId || 'sichuan';
	console.log('catId', catId)
    this.category = CATEGORIES.find(c => c.id === catId) || CATEGORIES[0];
	console.log('category', this.category)
    this.recipes = RECIPES.filter(r => r.cuisine === catId);
	console.log('recipes', this.recipes)
    // if (this.recipes.length === 0) this.recipes = RECIPES.slice(0, 4);
  },
  methods: {
    goBack() { uni.navigateBack(); },
    goToDetail(r) { uni.navigateTo({ url: `/pages/recipe-detail/index?id=${r.id}` }); }
  }
}
</script>

<style scoped>
.list-container { min-height: 100vh; background-color: #f5f3f0; padding-bottom: 80rpx; }
.status-bar { height: var(--status-bar-height); }

.nav-bar { background-color: rgba(245, 243, 240, 0.9); backdrop-filter: blur(10px); position: sticky; top: 0; z-index: 100; }
.nav-content { height: 100rpx; display: flex; align-items: center; justify-content: space-between; padding: 0 40rpx; }
.back-btn { color: #379587; width: 60rpx; }
.nav-title { font-size: 32rpx; font-weight: bold; color: #111817; }
.placeholder { width: 60rpx; }

.list-header { padding: 40rpx; margin-bottom: 20rpx; }
.header-sub { font-size: 20rpx; color: #379587; font-weight: 900; letter-spacing: 6rpx; display: block; }
.header-main { font-size: 56rpx; font-weight: 800; color: #111817; font-family: 'serif'; margin-top: 10rpx; display: block; }

.recipe-grid { display: flex; flex-wrap: wrap; padding: 0 30rpx; justify-content: space-between; }
.recipe-card { width: 330rpx; margin-bottom: 50rpx; background: #ffffff; border-radius: 40rpx; overflow: hidden; box-shadow: 0 10rpx 30rpx rgba(0,0,0,0.03); }
.full-card { width: 100%; display: flex; height: 320rpx; margin-bottom: 60rpx; }

.img-wrap { position: relative; width: 100%; height: 330rpx; }
.full-card .img-wrap { width: 45%; height: 100%; }
.card-img { width: 100%; height: 100%; }

.card-badge { position: absolute; top: 20rpx; left: 20rpx; background: #379587; color: white; font-size: 16rpx; font-weight: 900; padding: 4rpx 16rpx; border-radius: 8rpx; }
.card-info-overlay { position: absolute; bottom: 20rpx; left: 20rpx; right: 20rpx; display: flex; gap: 10rpx; }
.card-time, .card-difficulty { background: rgba(255,255,255,0.9); font-size: 18rpx; font-weight: bold; color: #333; padding: 4rpx 12rpx; border-radius: 8rpx; }

.card-body { padding: 24rpx; flex: 1; display: flex; flex-direction: column; justify-content: center; }
.card-name { font-size: 32rpx; font-weight: bold; color: #111817; display: block; }
.card-tagline { font-size: 22rpx; color: #999; font-style: italic; margin-top: 10rpx; display: block; }

.card-footer { margin-top: 20rpx; display: flex; align-items: center; color: #379587; }
.footer-link { font-size: 20rpx; font-weight: 900; border-bottom: 2rpx solid #379587; margin-right: 6rpx; }
.footer-icon { font-size: 24rpx; }
</style>
