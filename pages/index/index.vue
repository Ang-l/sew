<template>
  <view class="page-container">
    <!-- 状态栏占位 -->
    <view class="status-bar"></view>
    
    <!-- 头部：杂志风格 -->
    <view class="header">
      <view class="header-left">
        <text class="brand-sub">Simply Eat Well</text>
        <!-- <text class="brand-main">好好吃饭</text> -->
      </view>
      <view class="search-toggle" :class="{'active': isSearching}" @tap="toggleSearch">
        <text class="material-symbols-outlined">{{ isSearching ? 'close' : 'search' }}</text>
      </view>
    </view>

    <!-- 动态搜索框 -->
    <view class="search-area" :class="{'search-area-show': isSearching}">
      <view class="search-input-box">
        <text class="material-symbols-outlined search-inner-icon">search</text>
        <input 
          type="text" 
          v-model="searchQuery" 
          placeholder="搜索菜名或食材 (如: 豆腐)" 
          class="input-field"
          placeholder-style="color: #ccc;"
          :focus="isSearching"
        />
        <text v-if="searchQuery" class="material-symbols-outlined clear-icon" @tap="clearSearch">cancel</text>
      </view>
    </view>

    <!-- 搜索结果视图 -->
    <view v-if="searchQuery" class="search-results animate-fade">
      <view class="results-header">
        <text class="results-count">{{ filteredRecipes.length }} 个发现</text>
        <view class="results-line"></view>
      </view>
      
      <view v-if="filteredRecipes.length > 0" class="results-list">
        <view v-for="r in filteredRecipes" :key="r.id" class="search-item" @tap="goToDetail(r)">
          <image :src="r.image" mode="aspectFill" class="item-img" />
          <view class="item-info">
            <text class="item-name">{{r.name}}</text>
            <text class="item-tagline">{{r.tagline}}</text>
            <view class="item-meta">
              <text class="meta-txt">{{r.prepTime}}</text>
              <text class="meta-dot">·</text>
              <text class="meta-txt">{{r.difficulty}}</text>
            </view>
          </view>
        </view>
      </view>
      
      <!-- 无结果占位 -->
      <view v-else class="empty-state">
        <text class="material-symbols-outlined empty-icon">restaurant_menu</text>
        <text class="empty-text">未找到相关灵感</text>
      </view>
    </view>

    <!-- 默认首页视图：当没有搜索内容时展示 -->
    <view v-else class="home-main-content animate-fade">
      <!-- 核心封面图 -->
      <view class="hero-section" @tap="goToDetail(featuredRecipe)">
        <view class="hero-card">
          <image :src="featuredRecipe.image" mode="aspectFill" class="hero-img" />
          <view class="hero-overlay">
            <view class="tag-pill">今日封面</view>
            <text class="hero-title">{{featuredRecipe.name}}</text>
            <text class="hero-tagline">“ {{featuredRecipe.tagline}} ”</text>
          </view>
        </view>
      </view>

      <!-- 分类滑动区 -->
      <view class="section-box">
        <view class="section-header">
          <text class="section-title">灵感集</text>
          <text class="more-link" @tap="goToCategories">全部分类</text>
        </view>
        <scroll-view scroll-x class="cat-scroll" :show-scrollbar="false">
          <view v-for="cat in categories" :key="cat.id" class="cat-item" @tap="goToList(cat)">
            <view class="cat-circle">
              <image :src="cat.image" mode="aspectFill" class="cat-img" />
            </view>
            <text class="cat-name">{{cat.name}}</text>
          </view>
        </scroll-view>
      </view>

      <!-- 瀑布流推荐 -->
      <view class="recommend-grid">
        <view v-for="(r, index) in recommendations" :key="r.id" 
              class="recipe-card" 
              :class="{'offset-top': index % 2 !== 0}"
              @tap="goToDetail(r)">
          <view class="recipe-img-box">
            <image :src="r.image" mode="aspectFill" class="recipe-img" />
            <view class="recipe-time">{{r.prepTime}}</view>
          </view>
          <text class="recipe-name">{{r.name}}</text>
          <text class="recipe-sub">{{r.tagline}}</text>
        </view>
      </view>
    </view>

    <!-- 底部悬浮导航 -->
    <view class="floating-nav">
      <view class="nav-bar">
        <view class="nav-btn active">
          <text class="material-symbols-outlined">home</text>
          <text class="nav-label">首页</text>
        </view>
        <view class="nav-btn" @tap="goToProfile">
          <text class="material-symbols-outlined">person</text>
          <text class="nav-label">我的</text>
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
      categories: CATEGORIES,
      featuredRecipe: RECIPES.find(r => r.isFeatured) || RECIPES[0],
      recommendations: RECIPES.filter(r => !r.isFeatured).slice(0, 4),
      isSearching: false,
      searchQuery: ''
    }
  },
  computed: {
    // 核心搜索逻辑：匹配名称或配料
    filteredRecipes() {
      const query = this.searchQuery.trim().toLowerCase();
      if (!query) return [];
      
      return RECIPES.filter(recipe => {
        const nameMatch = recipe.name.toLowerCase().includes(query);
        const ingredientMatch = recipe.ingredients.some(ing => 
          ing.item.toLowerCase().includes(query)
        );
        return nameMatch || ingredientMatch;
      });
    }
  },
  methods: {
    toggleSearch() {
      this.isSearching = !this.isSearching;
      if (!this.isSearching) {
        this.searchQuery = '';
      }
    },
    clearSearch() {
      this.searchQuery = '';
    },
    goToDetail(r) { uni.navigateTo({ url: `/pages/recipe-detail/index?id=${r.id}` }); },
    goToList(c) { uni.navigateTo({ url: `/pages/recipe-list/index?catId=${c.id}` }); },
    goToCategories() { uni.navigateTo({ url: '/pages/categories/index' }); },
    goToProfile() { uni.redirectTo({ url: '/pages/profile/index' }); }
  }
}
</script>

<style>
/* 容器基础样式 */
.page-container {
  min-height: 100vh;
  background-color: #f5f3f0;
  padding-bottom: 200rpx;
}
.status-bar { height: var(--status-bar-height); }

/* 头部样式 */
.header {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  padding: 80rpx 40rpx 40rpx;
}
.brand-sub {
  font-size: 20rpx;
  color: #379587;
  font-weight: 900;
  letter-spacing: 6rpx;
}
.brand-main {
  font-size: 60rpx;
  font-weight: 800;
  color: #111817;
  font-family: 'serif';
}
.search-toggle {
  width: 90rpx;
  height: 90rpx;
  background: #ffffff;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 10rpx 30rpx rgba(0,0,0,0.05);
  transition: all 0.3s ease;
}
.search-toggle.active {
  background: #379587;
  color: #ffffff;
  transform: rotate(90deg);
}

/* 搜索输入区域 */
.search-area {
  padding: 0 40rpx;
  height: 0;
  overflow: hidden;
  opacity: 0;
  transition: all 0.4s cubic-bezier(0.165, 0.84, 0.44, 1);
}
.search-area-show {
  height: 120rpx;
  opacity: 1;
  margin-bottom: 20rpx;
}
.search-input-box {
  background: #ffffff;
  height: 100rpx;
  border-radius: 30rpx;
  display: flex;
  align-items: center;
  padding: 0 30rpx;
  box-shadow: inset 0 2rpx 10rpx rgba(0,0,0,0.05);
}
.search-inner-icon {
  color: #ccc;
  font-size: 40rpx;
  margin-right: 20rpx;
}
.input-field {
  flex: 1;
  font-size: 28rpx;
  font-weight: 600;
  color: #333;
}
.clear-icon {
  color: #eee;
  font-size: 36rpx;
}

/* 搜索结果 */
.search-results {
  padding: 20rpx 40rpx;
}
.results-header {
  display: flex;
  align-items: center;
  margin-bottom: 40rpx;
}
.results-count {
  font-size: 18rpx;
  font-weight: 900;
  color: #bbb;
  letter-spacing: 4rpx;
  text-transform: uppercase;
  margin-right: 20rpx;
  white-space: nowrap;
}
.results-line {
  flex: 1;
  height: 1rpx;
  background: #eee;
}

.search-item {
  display: flex;
  align-items: center;
  background: #ffffff;
  border-radius: 40rpx;
  padding: 20rpx;
  margin-bottom: 30rpx;
  box-shadow: 0 4rpx 20rpx rgba(0,0,0,0.02);
}
.item-img {
  width: 140rpx;
  height: 140rpx;
  border-radius: 30rpx;
  margin-right: 30rpx;
}
.item-info {
  flex: 1;
}
.item-name {
  font-size: 32rpx;
  font-weight: bold;
  color: #111817;
  display: block;
}
.item-tagline {
  font-size: 22rpx;
  color: #999;
  font-style: italic;
  margin-top: 6rpx;
  display: block;
}
.item-meta {
  display: flex;
  align-items: center;
  margin-top: 10rpx;
}
.meta-txt {
  font-size: 18rpx;
  font-weight: 900;
  color: #379587;
  letter-spacing: 2rpx;
}
.meta-dot {
  margin: 0 10rpx;
  color: #eee;
}

.empty-state {
  text-align: center;
  padding-top: 100rpx;
  opacity: 0.2;
}
.empty-icon {
  font-size: 80rpx;
  margin-bottom: 20rpx;
}
.empty-text {
  font-size: 24rpx;
  font-weight: 900;
  letter-spacing: 4rpx;
}

/* 动画效果 */
.animate-fade {
  animation: fadeIn 0.5s ease-out forwards;
}
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10rpx); }
  to { opacity: 1; transform: translateY(0); }
}

/* 封面卡片 */
.hero-section { padding: 0 40rpx; margin-bottom: 60rpx; }
.hero-card {
  position: relative;
  height: 400rpx;
  border-radius: 60rpx;
  overflow: hidden;
  box-shadow: 0 20rpx 50rpx rgba(0,0,0,0.1);
}
.hero-img { width: 100%; height: 100%; }
.hero-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
  padding: 40rpx;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}
.tag-pill {
  background: #379587;
  color: white;
  font-size: 18rpx;
  padding: 6rpx 20rpx;
  border-radius: 100rpx;
  width: fit-content;
  margin-bottom: 16rpx;
  font-weight: bold;
}
.hero-title { color: white; font-size: 44rpx; font-weight: bold; }
.hero-tagline { color: rgba(255,255,255,0.7); font-size: 24rpx; margin-top: 10rpx; font-style: italic; }

/* 分类滚动 */
.section-box { margin-bottom: 60rpx; }
.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 40rpx;
  margin-bottom: 30rpx;
}
.section-title { font-size: 36rpx; font-weight: bold; color: #111817; }
.more-link { font-size: 22rpx; color: #379587; font-weight: bold; }
.cat-scroll { white-space: nowrap; padding-left: 40rpx; }
.cat-item {
  display: inline-block;
  margin-right: 40rpx;
  text-align: center;
}
.cat-circle {
  width: 120rpx;
  height: 120rpx;
  border-radius: 50%;
  border: 4rpx solid #ffffff;
  overflow: hidden;
  box-shadow: 0 10rpx 20rpx rgba(0,0,0,0.05);
}
.cat-img { width: 100%; height: 100%; }
.cat-name { font-size: 22rpx; font-weight: bold; color: #999; margin-top: 16rpx; display: block; }

/* 推荐网格 */
.recommend-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  padding: 0 40rpx;
}
.recipe-card { width: 46%; margin-bottom: 40rpx; }
.offset-top { margin-top: 60rpx; }
.recipe-img-box {
  height: 380rpx;
  border-radius: 40rpx;
  overflow: hidden;
  position: relative;
  box-shadow: 0 10rpx 30rpx rgba(0,0,0,0.05);
}
.recipe-img { width: 100%; height: 100%; }
.recipe-time {
  position: absolute;
  top: 20rpx;
  left: 20rpx;
  background: rgba(255,255,255,0.9);
  padding: 4rpx 16rpx;
  border-radius: 20rpx;
  font-size: 18rpx;
  font-weight: bold;
  color: #379587;
}
.recipe-name { font-size: 30rpx; font-weight: bold; margin-top: 20rpx; display: block; }
.recipe-sub { font-size: 20rpx; color: #bbb; margin-top: 6rpx; display: block; }

/* 底部导航 */
.floating-nav {
  position: fixed;
  bottom: 60rpx;
  left: 60rpx;
  right: 60rpx;
  z-index: 999;
}
.nav-bar {
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(20rpx);
  border-radius: 100rpx;
  height: 120rpx;
  display: flex;
  justify-content: space-around;
  align-items: center;
  box-shadow: 0 20rpx 60rpx rgba(0,0,0,0.1);
  border: 1px solid rgba(255,255,255,0.5);
}
.nav-btn { display: flex; flex-direction: column; align-items: center; color: #9ca3af; }
.nav-btn.active { color: #379587; }
.nav-label { font-size: 18rpx; font-weight: bold; margin-top: 4rpx; }
</style>