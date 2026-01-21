<template>
  <view class="profile-container">
    <view class="status-bar"></view>
    
    <!-- 顶部极简背景 -->
    <view class="hero-bg"></view>

    <!-- 精致头像与姓名区 -->
    <view class="editorial-header">
      <view class="header-main-row">
        <view class="avatar-window">
          <image src="/static/logo.png" mode="aspectFill" class="avatar-img" />
          <view class="window-border"></view>
        </view>
        <view class="name-box">
          <view class="name-decorator"></view>
          <text class="user-title">好好吃饭</text>
          <view class="badge-row">
            <text class="tag">EST. 2026</text>
            <text class="tag-dot">•</text>
            <text class="tag">Simply Eat Well</text>
          </view>
        </view>
      </view>
      <text class="quote-text">“ 烹饪是一场通往灵魂的远行，每一道菜都有它未讲完的故事。 ”</text>
    </view>

    <!-- 功能列表：极简线性风格 -->
    <view class="menu-container">
      <!-- <view class="menu-group">
        <view class="menu-label">CONTENT / 内容</view>
        <view class="menu-list-card">
          <view class="menu-item" @tap="handleAction('favorites')">
            <view class="item-inner">
              <text class="material-symbols-outlined icon">bookmark</text>
              <text class="label">我的私人收藏</text>
            </view>
            <text class="material-symbols-outlined arrow">east</text>
          </view>
          <view class="menu-item" @tap="handleAction('history')">
            <view class="item-inner">
              <text class="material-symbols-outlined icon">explore</text>
              <text class="label">寻味足迹</text>
            </view>
            <text class="material-symbols-outlined arrow">east</text>
          </view>
        </view>
      </view> -->

      <view class="menu-group">
        <!-- <view class="menu-label">PREFERENCE / 设置</view> -->
        <view class="menu-list-card">
<!--          <view class="menu-item" @tap="handleAction('settings')">
            <view class="item-inner">
              <text class="material-symbols-outlined icon">tune</text>
              <text class="label">偏好与设置</text>
            </view>
            <text class="material-symbols-outlined arrow">east</text>
          </view> -->
          <view class="menu-item" @tap="goToys()">
            <view class="item-inner">
              <text class="material-symbols-outlined icon">auto_awesome</text>
              <text class="label">免责声明</text>
            </view>
            <text class="material-symbols-outlined arrow">east</text>
          </view>
        </view>
      </view>
    </view>

    <!-- 底部版权 -->
    <view class="minimal-footer">
      <text class="footer-brand">CULINARY STUDIO</text>
      <text class="footer-tag">PREMIUM VERSION 1.2.0</text>
    </view>

    <!-- 全局统一底部导航 -->
    <view class="bottom-nav-wrap">
      <view class="nav-inner">
        <view class="nav-tab" @tap="goToHome">
          <text class="material-symbols-outlined">home</text>
          <text class="nav-text">探索</text>
        </view>
        <view class="nav-tab active">
          <text class="material-symbols-outlined filled">person</text>
          <text class="nav-text">我的</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  methods: {
    goToHome() {
      uni.redirectTo({
        url: '/pages/index/index',
        animationType: 'fade-in'
      });
    },
	goToys() {
	  uni.navigateTo({ url: '/pages/disclaimer/index' });
	},
    handleAction(type) {
      uni.showToast({
        title: '已开启云端同步',
        icon: 'none'
      });
    }
  }
}
</script>

<style scoped>
.profile-container {
  min-height: 100vh;
  background-color: #f5f3f0;
  padding-bottom: 240rpx;
  position: relative;
}
.status-bar { height: var(--status-bar-height); }

.hero-bg {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 500rpx;
  background: linear-gradient(180deg, #ffffff 0%, rgba(245, 243, 240, 0) 100%);
  z-index: 0;
}

/* 杂志头部排版 */
.editorial-header {
  position: relative;
  z-index: 1;
  padding: 120rpx 60rpx 60rpx;
}

.header-main-row {
  display: flex;
  align-items: flex-end;
  margin-bottom: 40rpx;
}

/* 缩小的艺廊方窗头像 */
.avatar-window {
  position: relative;
  width: 150rpx;
  height: 180rpx; /* 非对称比例更高级 */
  margin-right: 40rpx;
  box-shadow: 0 20rpx 40rpx rgba(0,0,0,0.1);
}
.avatar-img {
  width: 100%;
  height: 100%;
  border-radius: 20rpx;
}
.window-border {
  position: absolute;
  inset: -10rpx;
  border: 1rpx solid #379587;
  border-radius: 24rpx;
  opacity: 0.3;
  z-index: -1;
}

.name-box {
  flex: 1;
  padding-bottom: 10rpx;
}
.name-decorator {
  width: 40rpx;
  height: 4rpx;
  background: #379587;
  margin-bottom: 16rpx;
}
.user-title {
  font-size: 52rpx;
  font-weight: 800;
  color: #111817;
  font-family: 'serif';
  letter-spacing: -2rpx;
  display: block;
}
.badge-row {
  display: flex;
  align-items: center;
  gap: 12rpx;
  margin-top: 12rpx;
}
.tag {
  font-size: 16rpx;
  font-weight: 900;
  color: #379587;
  letter-spacing: 4rpx;
}
.tag-dot { font-size: 16rpx; color: #ddd; }

.quote-text {
  font-size: 24rpx;
  color: #999;
  font-style: italic;
  line-height: 1.8;
  margin-top: 40rpx;
  display: block;
  border-left: 2rpx solid #eee;
  padding-left: 30rpx;
}

/* 列表区域 */
.menu-container {
  padding: 0 60rpx;
}
.menu-group {
  margin-bottom: 60rpx;
}
.menu-label {
  font-size: 18rpx;
  font-weight: 900;
  color: #bbb;
  letter-spacing: 6rpx;
  margin-bottom: 30rpx;
  margin-left: 4rpx;
}

.menu-list-card {
  background: #ffffff;
  border-radius: 40rpx;
  padding: 10rpx 40rpx;
  box-shadow: 0 10rpx 30rpx rgba(0,0,0,0.02);
}

.menu-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 40rpx 0;
}
.menu-item:not(:last-child) {
  border-bottom: 1rpx solid #f9f9f9;
}

.item-inner {
  display: flex;
  align-items: center;
}
.icon {
  font-size: 40rpx;
  color: #379587;
  margin-right: 30rpx;
}
.label {
  font-size: 30rpx;
  font-weight: 600;
  color: #333;
}
.arrow {
  font-size: 32rpx;
  color: #eee;
  transition: all 0.3s ease;
}
.menu-item:active .arrow {
  color: #379587;
  transform: translateX(10rpx);
}

/* 底部声明 */
.minimal-footer {
  text-align: center;
  padding: 60rpx 0;
}
.footer-brand {
  font-size: 18rpx;
  font-weight: 900;
  color: #ddd;
  letter-spacing: 12rpx;
  display: block;
}
.footer-tag {
  font-size: 14rpx;
  color: #eee;
  margin-top: 10rpx;
  display: block;
}

/* 底部导航 */
.bottom-nav-wrap {
  position: fixed;
  bottom: 60rpx;
  left: 60rpx;
  right: 60rpx;
  z-index: 1000;
}
.nav-inner {
  background: rgba(255, 255, 255, 0.98);
  backdrop-filter: blur(20rpx);
  height: 124rpx;
  border-radius: 100rpx;
  display: flex;
  justify-content: space-around;
  align-items: center;
  box-shadow: 0 30rpx 70rpx rgba(0,0,0,0.08);
  border: 1px solid rgba(255,255,255,0.8);
}
.nav-tab {
  display: flex;
  flex-direction: column;
  align-items: center;
  color: #cbd5e1;
}
.nav-tab.active { color: #379587; }
.nav-text { font-size: 18rpx; font-weight: 900; margin-top: 8rpx; letter-spacing: 2rpx; }
</style>