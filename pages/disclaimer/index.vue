<template>
  <view class="disclaimer-container">
    <view class="status-bar"></view>
    
    <!-- 顶部导航 -->
    <view class="nav-bar">
      <view class="back-btn" @tap="goBack">
        <text class="material-symbols-outlined">arrow_back_ios_new</text>
      </view>
      <text class="nav-title">免责声明</text>
      <view class="placeholder"></view>
    </view>

    <view class="content-scroll">
      <view class="hero-header">
        <text class="header-sub">LEGAL & PRIVACY</text>
        <text class="header-main">关于工坊的申明</text>
        <view class="header-line"></view>
      </view>

      <view class="statement-card">
        <!-- 板块 1: 数据来源 -->
        <view class="section">
          <view class="section-tag">01 / 数据来源与整理</view>
          <text class="text-p">本应用所展示的菜谱内容与相关信息，来源于公开网络资料的整理与二次结构化处理，主要数据来源包括但不限于以下公开项目与站点：</text>
          <view class="link-box">
            <text class="link-item">• CookLikeHOC 开源项目 (GitHub)</text>
            <text class="link-item">• 基于上述开源内容的学习站点</text>
          </view>
          <text class="text-p">应用内所使用的菜谱信息，均是在尊重原始资料的前提下，对内容进行整理、拆分、结构化转换与移动端展示适配后形成，仅用于学习、交流与技术展示目的。</text>
        </view>

        <!-- 板块 2: 项目性质 -->
        <view class="section">
          <view class="section-tag">02 / 项目性质与关联</view>
          <text class="text-p">本应用为非官方、非授权的个人学习与技术展示项目，与任何餐饮品牌、企业、机构或组织（包括但不限于“老乡鸡”或其他可能被提及的品牌）不存在任何形式的隶属关系、授权关系、合作关系或商业关联。</text>
          <text class="text-p">应用中出现的菜名、描述、图片链接及相关内容，仅用于菜谱内容识别与学习参考，不构成任何商业宣传、品牌背书或经营行为。</text>
        </view>

        <!-- 板块 3: 盈利申明 -->
        <view class="section">
          <view class="section-tag">03 / 非商业化声明</view>
          <text class="text-p">本应用不以盈利为目的，不提供任何形式的付费功能，不进行菜谱内容售卖，不通过应用内菜谱数据、图片或相关内容获取直接或间接的商业收益。</text>
          <text class="text-p">若未来应用形态或使用场景发生变化，涉及商业用途或其他可能产生收益的情况，将依法依规对相关内容进行调整、替换、授权确认或下架处理。</text>
        </view>

        <!-- 板块 4: 风险提示 -->
        <view class="section">
          <view class="section-tag">04 / 风险提示与责任免除</view>
          <text class="text-p">应用内所展示的菜谱内容来源于公开资料整理，无法保证其完整性、准确性、时效性或适用于所有实际烹饪场景。</text>
          <text class="text-p">用户在实际烹饪过程中，应根据自身经验、食材条件、身体状况及食品安全规范自行判断和操作。本应用不对因使用或参考应用内菜谱内容而产生的任何直接或间接后果承担责任。</text>
        </view>

        <!-- 板块 5: 联系反馈 -->
        <view class="section contact-section">
          <view class="section-tag">05 / 版权反馈与联系</view>
          <text class="text-p">如相关权利人认为应用内部分内容在版权标注、使用方式或展示形式上存在不当之处，请联系开发者。</text>
          <view class="email-badge">
            <text class="material-symbols-outlined email-icon">mail</text>
            <text class="email-text">angnumber995@gmail.com</text>
          </view>
        </view>
      </view>

      <view class="footer-sign">
        <text class="sign-text">CULINARY STUDIO DEVELOPMENT TEAM</text>
        <text class="date-text">UPDATED AT 2026.01</text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  methods: {
    goBack() { uni.navigateBack(); }
  }
}
</script>

<style scoped>
.disclaimer-container {
  min-height: 100vh;
  background-color: #f5f3f0;
}
.status-bar { height: var(--status-bar-height); }

.nav-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20rpx 40rpx;
  background-color: #f5f3f0;
}
.back-btn { color: #379587; width: 60rpx; }
.nav-title { font-size: 30rpx; font-weight: bold; font-family: 'serif'; }
.placeholder { width: 60rpx; }

.content-scroll {
  padding: 60rpx 40rpx 100rpx;
}

.hero-header {
  margin-bottom: 80rpx;
}
.header-sub {
  font-size: 18rpx;
  color: #379587;
  font-weight: 900;
  letter-spacing: 8rpx;
  display: block;
}
.header-main {
  font-size: 52rpx;
  font-weight: 800;
  color: #111817;
  font-family: 'serif';
  margin-top: 10rpx;
  display: block;
}
.header-line {
  width: 60rpx;
  height: 6rpx;
  background: #379587;
  margin-top: 30rpx;
}

.statement-card {
  background: #ffffff;
  border-radius: 60rpx;
  padding: 60rpx 50rpx;
  box-shadow: 0 20rpx 60rpx rgba(0,0,0,0.03);
}

.section {
  margin-bottom: 60rpx;
}
.section-tag {
  font-size: 16rpx;
  font-weight: 900;
  color: #379587;
  background: rgba(55, 149, 135, 0.08);
  padding: 4rpx 16rpx;
  border-radius: 6rpx;
  width: fit-content;
  margin-bottom: 24rpx;
  letter-spacing: 2rpx;
}
.text-p {
  font-size: 26rpx;
  color: #444;
  line-height: 1.8;
  display: block;
  margin-bottom: 20rpx;
  text-align: justify;
}

.link-box {
  background: #f9f9f9;
  padding: 24rpx;
  border-radius: 20rpx;
  margin: 20rpx 0;
}
.link-item {
  font-size: 22rpx;
  color: #888;
  display: block;
  margin-bottom: 10rpx;
}

.contact-section {
  padding-top: 40rpx;
  border-top: 1rpx solid #f0f0f0;
}

.email-badge {
  display: flex;
  align-items: center;
  background: #111817;
  padding: 24rpx 40rpx;
  border-radius: 100rpx;
  margin-top: 30rpx;
  width: fit-content;
}
.email-icon {
  color: #379587;
  font-size: 32rpx;
  margin-right: 16rpx;
}
.email-text {
  color: #fff;
  font-size: 24rpx;
  font-weight: bold;
}

.footer-sign {
  margin-top: 100rpx;
  text-align: center;
}
.sign-text {
  font-size: 14rpx;
  font-weight: 900;
  color: #ddd;
  letter-spacing: 4rpx;
  display: block;
}
.date-text {
  font-size: 14rpx;
  color: #eee;
  margin-top: 10rpx;
  display: block;
}
</style>