<template>
  <view class="detail-container" v-if="recipe.id">
    <!-- 悬浮返回 -->
    <view class="back-btn-fixed" @tap="goBack">
      <text class="material-symbols-outlined">arrow_back_ios_new</text>
    </view>

    <!-- 顶端大图：改为完整显示模式 -->
    <view class="hero-box">
      <image :src="recipe.image" mode="widthFix" class="hero-img" />
      <view class="hero-mask"></view>
    </view>

    <!-- 内容区域 -->
    <view class="content-body">
      <!-- 核心信息卡片 -->
      <view class="info-card">
        <text class="card-badge">GOURMET SELECTION</text>
        <text class="recipe-title">{{recipe.name}}</text>
        <text class="recipe-tagline">“ {{recipe.tagline}} ”</text>
        
        <view class="stats-row">
          <view class="stat-item">
            <text class="stat-label">准备时长</text>
            <text class="stat-val">{{recipe.prepTime}}</text>
          </view>
          <view class="stat-divider"></view>
          <view class="stat-item">
            <text class="stat-label">难度系数</text>
            <text class="stat-val">{{recipe.difficulty}}</text>
          </view>
          <view class="stat-divider"></view>
          <view class="stat-item">
            <text class="stat-label">热量估算</text>
            <text class="stat-val">{{recipe.calories}}</text>
          </view>
        </view>
      </view>

      <!-- 食材部分 -->
      <view class="section">
        <view class="section-title-box">
          <view class="title-dot"></view>
          <text class="section-title">所需食材</text>
        </view>
        <view class="ingredients-wrap">
          <view v-for="(ing, i) in recipe.ingredients" :key="i" class="ing-item">
            <text class="ing-name">{{ing.item}}</text>
            <text class="ing-amount">{{ing.amount}}</text>
          </view>
        </view>
      </view>

      <!-- 步骤部分 -->
      <view class="section">
        <view class="section-title-box">
          <view class="title-dot"></view>
          <text class="section-title">烹饪步骤</text>
        </view>
        <view class="steps-wrap">
          <view v-for="(step, i) in recipe.steps" :key="i" class="step-card">
            <view class="step-index">{{i + 1}}</view>
            <view class="step-info">
              <text class="step-t">{{step.title}}</text>
              <text class="step-d">{{step.desc}}</text>
            </view>
          </view>
        </view>
      </view>

      <!-- 手绘制作流程 如果存在手绘图就直接拿到不存在就不拿了 -->
      <view class="section sketch-section" v-if="recipe.paper">
        <view class="section-title-box">
          <view class="title-dot"></view>
          <view class="sketch-title-group">
            <text class="section-title">手绘制作流程</text>
            <text class="sketch-subtitle">CHEF'S SKETCH</text>
          </view>
        </view>
        <view class="sketch-paper">
          <image :src="recipe.paper" mode="widthFix" class="sketch-img" />
          <view class="sketch-overlay">
            <text class="sketch-note">灵感源自四季的馈赠，每一份火候都是对食材的极致礼赞。</text>
            <view class="sketch-signature">Culinary Studio / 2024</view>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
import { RECIPES } from '../../common/constants';

export default {
  data() {
    return {
      recipe: {}
    }
  },
  onLoad(options) {
    const id = options.id;
    this.recipe = RECIPES.find(r => r.id === id) || RECIPES[0];
  },
  methods: {
    goBack() { uni.navigateBack(); }
  }
}
</script>

<style scoped>
.detail-container { background-color: #f5f3f0; min-height: 100vh; padding-bottom: 120rpx; }

/* 返回按钮 */
.back-btn-fixed {
  position: fixed;
  top: 60rpx;
  left: 40rpx;
  z-index: 100;
  width: 90rpx;
  height: 90rpx;
  background: rgba(255,255,255,0.8);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #379587;
  box-shadow: 0 10rpx 30rpx rgba(0,0,0,0.1);
  backdrop-filter: blur(10rpx);
}

/* 顶部图片：改为自适应高度以显示全部图片 */
.hero-box { width: 100%; position: relative; background-color: #fff; }
.hero-img { width: 100%; display: block; }
.hero-mask { 
  position: absolute; 
  left: 0;
  right: 0;
  bottom: 0;
  height: 200rpx;
  background: linear-gradient(to bottom, transparent, #f5f3f0); 
}

/* 内容主体 */
.content-body { position: relative; padding: 0 40rpx; margin-top: -60rpx; z-index: 10; }

/* 信息卡片 */
.info-card {
  background: #ffffff;
  border-radius: 60rpx;
  padding: 80rpx 40rpx 60rpx;
  text-align: center;
  box-shadow: 0 30rpx 80rpx rgba(0,0,0,0.08);
  margin-bottom: 60rpx;
}
.card-badge { font-size: 18rpx; color: #379587; font-weight: 900; letter-spacing: 6rpx; display: block; margin-bottom: 30rpx; }
.recipe-title { font-size: 56rpx; font-weight: bold; color: #111817; font-family: 'serif'; display: block; margin-bottom: 20rpx; }
.recipe-tagline { font-size: 26rpx; color: #999; font-style: italic; display: block; }

.stats-row { display: flex; align-items: center; justify-content: center; margin-top: 60rpx; padding-top: 40rpx; border-top: 2rpx solid #f0f0f0; }
.stat-item { flex: 1; }
.stat-label { font-size: 18rpx; color: #bbb; font-weight: bold; display: block; margin-bottom: 10rpx; }
.stat-val { font-size: 28rpx; font-weight: bold; color: #333; }
.stat-divider { width: 2rpx; height: 60rpx; background: #eee; }

/* 章节通用样式 */
.section { margin-bottom: 80rpx; }
.section-title-box { display: flex; align-items: center; margin-bottom: 40rpx; }
.title-dot { width: 16rpx; height: 16rpx; background: #379587; border-radius: 50%; margin-right: 20rpx; }
.section-title { font-size: 40rpx; font-weight: bold; color: #111817; font-family: 'serif'; }

/* 食材列表 */
.ing-item {
  background: #ffffff;
  border-radius: 30rpx;
  padding: 30rpx 40rpx;
  display: flex;
  justify-content: space-between;
  margin-bottom: 20rpx;
  box-shadow: 0 4rpx 10rpx rgba(0,0,0,0.02);
}
.ing-name { font-weight: bold; color: #444; font-size: 28rpx; }
.ing-amount { color: #379587; font-weight: 900; font-size: 28rpx; }

/* 步骤卡片 */
.step-card { display: flex; margin-bottom: 60rpx; }
.step-index {
  width: 80rpx;
  height: 80rpx;
  background: rgba(55, 149, 135, 0.1);
  border-radius: 24rpx;
  color: #379587;
  font-weight: 900;
  font-size: 36rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  margin-right: 30rpx;
}
.step-t { font-size: 34rpx; font-weight: bold; color: #333; display: block; margin-bottom: 10rpx; }
.step-d { font-size: 28rpx; color: #666; line-height: 1.6; display: block; }

/* 主厨手稿样式 */
.sketch-section { margin-top: 100rpx; }
.sketch-title-group { display: flex; flex-direction: column; }
.sketch-subtitle { font-size: 16rpx; font-weight: 900; color: #bbb; letter-spacing: 4rpx; margin-top: 4rpx; }

.sketch-paper {
  position: relative;
  background: #fff;
  padding: 30rpx;
  border-radius: 4rpx;
  box-shadow: 0 10rpx 40rpx rgba(0,0,0,0.05);
  transform: rotate(-0.5deg);
  border: 1px solid rgba(0,0,0,0.05);
}
.sketch-img {
  width: 100%;
  height: auto; /* 移除固定高度，使用 widthFix */
  border-radius: 2rpx;
  filter: sepia(0.1) contrast(1.05);
}
.sketch-overlay {
  padding: 40rpx 20rpx 20rpx;
  text-align: center;
}
.sketch-note {
  font-size: 22rpx;
  color: #888;
  font-family: 'serif';
  font-style: italic;
  line-height: 1.6;
}
.sketch-signature {
  margin-top: 30rpx;
  font-size: 16rpx;
  font-weight: 900;
  color: #ccc;
  letter-spacing: 4rpx;
  text-transform: uppercase;
}
</style>