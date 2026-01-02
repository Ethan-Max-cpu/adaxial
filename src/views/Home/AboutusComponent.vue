<template>
  <div class="about-container">
    <!-- 桌面端布局 -->
    <div class="about-desktop">
      <h1 class="about-title">5 YEARS OF MARKETING DOMINATION</h1>
      <div class="stats-grid">
        <div class="stat-item">
          <div class="stat-value">$1.3 BILLION</div>
          <div class="stat-label">GROSS REVENUE</div>
        </div>
        <div class="stat-item">
          <div class="stat-value">$438,762,910+</div>
          <div class="stat-label">ANNUAL MEDIA SPEND</div>
        </div>
        <div class="stat-item">
          <div class="stat-value">4,000+</div>
          <div class="stat-label">BRAND SUCCESSFULLY</div>
        </div>
      </div>
    </div>

    <!-- 移动端布局 -->
    <div class="about-mobile">
      <h1 class="about-title">11 YEARS OF MARKETING DOMINATION</h1>
      <div class="stats-grid-mobile">
        <div class="stat-item-mobile">
          <div class="stat-value-mobile">$2.9 BILLION</div>
          <div class="stat-label-mobile">GROSS REVENUE</div>
        </div>
        <div class="stat-item-mobile">
          <div class="stat-value-mobile">$521,493,837+</div>
          <div class="stat-label-mobile">ANNUAL MEDIA SPEND</div>
        </div>
        <div class="stat-item-mobile">
          <div class="stat-value-mobile">5,000+</div>
          <div class="stat-label-mobile">BRANDS SUCCESSFULLY GROWN</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// 这个组件是纯展示型组件，不需要响应式数据
</script>

<style scoped>
/* 基础样式 - 要求1: 背景改为白色 */
.about-container {
  background-color: #ffffff; /* 改为白色背景 */
  color: #000000; /* 默认字体颜色改为黑色，适配白色背景 */
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
  min-height: auto;
  padding: 60px 20px;
  width: 100%;
  box-sizing: border-box;
}

/* 标题样式 - 适配白色背景 */
.about-title {
  font-size: 48px;
  font-weight: 700;
  text-align: center;
  margin-bottom: 60px;
  color: #000000; /* 适配白色背景，使用深色文字 */
  line-height: 1.2;
  letter-spacing: 1px;
  text-transform: uppercase;
}

/* 桌面端布局 - 默认显示 */
.about-desktop {
  display: block;
  max-width: 1200px;
  margin: 0 auto;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 40px;
  text-align: center;
}

.stat-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 30px 20px;
}

/* 要求3: 红色字体不变 */
.stat-value {
  font-size: 40px;
  font-weight: 700;
  color: #e63946; /* 红色字体保持原样 */
  margin-bottom: 15px;
  line-height: 1.2;
  letter-spacing: 0.5px;
}

/* 适配白色背景 */
.stat-label {
  font-size: 20px;
  font-weight: 600;
  color: #333333; /* 使用深灰色，适配白色背景，提高可读性 */
  line-height: 1.4;
  letter-spacing: 0.5px;
  text-transform: uppercase;
}

/* 移动端布局 - 默认隐藏 */
.about-mobile {
  display: none;
  width: 100%;
}

.stats-grid-mobile {
  display: flex;
  flex-direction: column;
  gap: 30px;
  width: 100%;
}

.stat-item-mobile {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 25px 15px;
  text-align: center;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1); /* 改为深色边框，适配白色背景 */
}

.stat-item-mobile:last-child {
  border-bottom: none;
}

/* 要求3: 红色字体不变 */
.stat-value-mobile {
  font-size: 32px;
  font-weight: 700;
  color: #e63946; /* 红色字体保持原样 */
  margin-bottom: 10px;
  line-height: 1.2;
  letter-spacing: 0.5px;
}

/* 适配白色背景 */
.stat-label-mobile {
  font-size: 18px;
  font-weight: 600;
  color: #333333; /* 使用深灰色，适配白色背景，提高可读性 */
  line-height: 1.4;
  letter-spacing: 0.5px;
  text-transform: uppercase;
}

/* 响应式设计 - 优化移动端适配 */
@media (max-width: 1024px) {
  .about-title {
    font-size: 40px;
    margin-bottom: 50px;
  }
  
  .stat-value {
    font-size: 36px;
  }
  
  .stat-label {
    font-size: 18px;
  }
}

/* 平板设备适配 */
@media (max-width: 768px) and (min-width: 641px) {
  .about-title {
    font-size: 36px;
    margin-bottom: 45px;
  }
  
  .stats-grid {
    grid-template-columns: repeat(3, 1fr);
    gap: 25px;
  }
  
  .stat-value {
    font-size: 30px;
  }
  
  .stat-label {
    font-size: 16px;
  }
}

/* 移动端适配 */
@media (max-width: 640px) {
  /* 隐藏桌面端，显示移动端 */
  .about-desktop {
    display: none;
  }
  
  .about-mobile {
    display: block;
  }
  
  .about-container {
    padding: 30px 16px;
  }
  
  .about-title {
    font-size: 24px;
    margin-bottom: 30px;
    letter-spacing: 0.5px;
    line-height: 1.3;
  }
  
  .stat-value-mobile {
    font-size: 28px;
  }
  
  .stat-label-mobile {
    font-size: 16px;
  }
  
  .stat-item-mobile {
    padding: 20px 0;
  }
}

/* 小屏幕手机适配 */
@media (max-width: 375px) {
  .about-title {
    font-size: 20px;
    margin-bottom: 25px;
  }
  
  .stat-item-mobile {
    padding: 18px 0;
  }
  
  .stat-value-mobile {
    font-size: 24px;
  }
  
  .stat-label-mobile {
    font-size: 14px;
  }
  
  .about-container {
    padding: 25px 12px;
  }
}

/* 平板中等屏幕适配 */
@media (min-width: 769px) and (max-width: 1024px) {
  .about-title {
    font-size: 36px;
  }
  
  .stat-value {
    font-size: 32px;
  }
  
  .stat-label {
    font-size: 18px;
  }
  
  .stats-grid {
    gap: 30px;
  }
}

/* 超大屏幕适配 */
@media (min-width: 1440px) {
  .about-container {
    padding: 80px 20px;
  }
  
  .about-title {
    font-size: 56px;
    margin-bottom: 80px;
  }
  
  .stat-value {
    font-size: 48px;
  }
  
  .stat-label {
    font-size: 24px;
  }
}

/* 极高分辨率适配 */
@media (min-width: 1920px) {
  .about-container {
    max-width: 1600px;
    margin: 0 auto;
  }
}
</style>