<template>
  <div class="promo-container">
    <!-- 内容容器，控制左右间距 -->
    <div class="content-wrapper">
      <!-- 第一部分：加粗标题 -->
      <h1 class="main-title">Agency accounts for all platforms</h1>
      
      <!-- 第二部分：正文 -->
      <p class="subtitle">Fastest turnarounds and best rates in the industry</p>
      
      <!-- 第三部分：图标展示 -->
      <div class="platform-icons">
        <div 
          v-for="(platform, index) in platforms" 
          :key="index" 
          class="platform-icon"
          :title="platform.name"
        >
          <!-- 通过链接引入本地图标文件 -->
          <img 
            :src="platform.icon" 
            :alt="platform.name" 
            class="platform-icon-img"
            @error="handleImageError(platform)"
          />
        </div>
      </div>
      
      <!-- 第四部分：按钮 -->
      <el-button 
        class="cta-button" 
        type="primary" 
        @click.prevent="scrollToPricing"
      >
        Get Started Now!
        <el-icon class="button-icon">
          <ArrowRight />
        </el-icon>
      </el-button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { ElButton, ElIcon } from 'element-plus'
import { ArrowRight } from '@element-plus/icons-vue'
import Bigo from '@/assets/images/Bigo.png'
import Bing from '@/assets/images/Bing.png'
import Facebook from '@/assets/images/Facebook.png'
import Google from '@/assets/images/Google.png'
import Newsbreak from '@/assets/images/Newsbreak.png'
import Snapchat from '@/assets/images/Snapchat.png'
import Taboola from '@/assets/images/Taboola.png'
import TikTok from '@/assets/images/TikTok.png'
import Twitter from '@/assets/images/Twitter.png'

// 响应式平台数据，确保顺序与图片一致
const platforms = ref([
  { 
    name: 'Facebook',
    icon: Facebook
  },
  { 
    name: 'TikTok',
    icon: TikTok
  },
  { 
    name: 'Google',
    icon: Google
  },
  { 
    name: 'Bigo',
    icon: Bigo
  },
  { 
    name: 'Taboola',
    icon: Taboola
  },
  { 
    name: 'Newsbreak',
    icon: Newsbreak
  },
  { 
    name: 'Snapchat',
    icon: Snapchat
  },
  { 
    name: 'Twitter',
    icon: Twitter
  },
  { 
    name: 'Bing',
    icon: Bing
  }
])

// 图标加载失败时的后备处理
const handleImageError = (platform) => {
  console.error(`Failed to load icon for ${platform.name}`)
  const iconDiv = event.target.parentElement
  iconDiv.innerHTML = `<span class="fallback-icon">${platform.name.charAt(0)}</span>`
  iconDiv.style.backgroundColor = '#f0f0f0'
  iconDiv.style.color = '#333'
}

// 平滑滚动到价格区域
const scrollToPricing = () => {
  const pricingElement = document.getElementById('pricing-section')
  if (pricingElement) {
    // 平滑滚动
    pricingElement.scrollIntoView({ 
      behavior: 'smooth',
      block: 'start'
    })
  }
}
</script>

<style scoped>
/* 组件横向占据整个屏幕 */
.promo-container {
  width: 100vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: white;
  position: relative;
  left: 50%;
  right: 50%;
  margin-left: -50vw;
  margin-right: -50vw;
  /* 移除所有垂直内外边距，使其紧凑 */
  margin-top: 0;
  margin-bottom: 0;
  padding-top: 0;
  padding-bottom: 0;
  box-sizing: border-box;
}

/* 内容容器，减小左右间距以确保9个图标在一行内 */
.content-wrapper {
  width: 100%;
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 clamp(10px, 3vw, 30px);
  text-align: center;
  box-sizing: border-box;
  /* 为内容添加一些垂直内边距，但不会与其他组件产生间隙 */
  padding-top: 20px;
  padding-bottom: 20px;
}

/* 第一部分：加粗标题 - 增加下边距避免覆盖 */
.main-title {
  font-size: clamp(2.8rem, 5.5vw, 3.8rem);
  font-weight: 900;
  color: #000000;
  margin: 0 0 20px 0; /* 从8px增加到20px，避免被覆盖 */
  line-height: 1.2; /* 从1.1恢复到1.2 */
  text-align: center;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 100%;
  width: 100%;
  padding: 0 5px;
  letter-spacing: -0.5px;
}

/* 第二部分：正文 - 适当增加下边距 */
.subtitle {
  font-size: clamp(1.3rem, 2.8vw, 1.7rem);
  color: #666666;
  margin: 0 0 40px 0; /* 从28px增加到40px */
  line-height: 1.4; /* 从1.3增加到1.4 */
  text-align: center;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 100%;
  width: 100%;
  padding: 0 5px;
  font-weight: 400;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  letter-spacing: 0.2px;
}

/* 第三部分：图标容器 - 适当增加下边距 */
.platform-icons {
  display: flex;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  gap: clamp(8px, 1.2vw, 12px);
  margin: 0 auto 40px auto; /* 从28px增加到40px */
  max-width: 1000px;
  width: 100%;
  padding: 0 5px;
  overflow: visible;
  flex-shrink: 0;
}

/* 单个平台图标 */
.platform-icon {
  width: clamp(48px, 6vw, 70px);
  height: clamp(48px, 6vw, 70px);
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: white;
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.08);
  transition: all 0.3s ease;
  cursor: pointer;
  flex-shrink: 0;
  overflow: hidden;
  position: relative;
  flex: 0 0 auto;
}

.platform-icon:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.12);
}

/* 图标图片样式 */
.platform-icon-img {
  width: 55%;
  height: 55%;
  object-fit: contain;
  filter: brightness(1) saturate(1);
  transition: transform 0.3s ease;
  position: relative;
  z-index: 1;
}

.platform-icon:hover .platform-icon-img {
  transform: scale(1.08);
}

/* 为透明背景的图标添加白色背景 */
.platform-icon::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: white;
  z-index: 0;
  border-radius: 8px;
}

/* 后备图标样式 */
.fallback-icon {
  font-weight: bold;
  font-size: 1.2rem;
  font-family: Arial, sans-serif;
  color: inherit;
}

/* 第四部分：按钮 - 移除额外外边距 */
.cta-button {
  background: linear-gradient(135deg, #10B981 0%, #059669 100%) !important;
  border: none !important;
  font-size: clamp(1.1rem, 2.2vw, 1.4rem);
  font-weight: 600;
  padding: clamp(14px, 2.2vw, 18px) clamp(30px, 3.5vw, 42px);
  border-radius: 10px;
  height: auto;
  transition: all 0.3s ease;
  color: white !important;
  box-shadow: 0 6px 20px rgba(16, 185, 129, 0.25);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  min-width: 200px;
  letter-spacing: 0.5px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  margin: 0; /* 确保按钮没有外边距 */
}

.cta-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 25px rgba(16, 185, 129, 0.35);
  background: linear-gradient(135deg, #059669 0%, #047857 100%) !important;
}

.cta-button:active {
  transform: translateY(-1px);
  box-shadow: 0 4px 15px rgba(16, 185, 129, 0.3);
}

.button-icon {
  font-size: 1.1em;
  transition: transform 0.3s ease;
  margin-left: 4px;
}

.cta-button:hover .button-icon {
  transform: translateX(4px);
}

/* 移动端适配 */
@media (max-width: 1200px) {
  .content-wrapper {
    max-width: 1000px;
    padding: 0 20px;
  }
  
  .platform-icons {
    max-width: 900px;
  }
}

@media (max-width: 1024px) {
  .content-wrapper {
    max-width: 900px;
    padding: 0 15px;
  }
  
  .platform-icons {
    max-width: 850px;
    gap: 10px;
  }
  
  .platform-icon {
    width: 52px;
    height: 52px;
  }
}

@media (max-width: 768px) {
  .promo-container {
    padding-top: 0;
    padding-bottom: 0;
  }
  
  .content-wrapper {
    padding: 0 12px;
    padding-top: 15px;
    padding-bottom: 15px;
  }
  
  /* 移动端允许标题和正文换行 */
  .main-title {
    white-space: normal;
    line-height: 1.3;
    font-size: 2.4rem;
    padding: 0 5px;
    margin-bottom: 16px; /* 移动端增加标题下边距 */
  }
  
  .subtitle {
    white-space: normal;
    line-height: 1.5;
    font-size: 1.3rem;
    padding: 0 5px;
    margin-bottom: 30px; /* 移动端增加正文下边距 */
  }
  
  .platform-icons {
    flex-wrap: wrap; /* 移动端允许换行 */
    gap: 12px;
    padding: 0 5px;
    margin-bottom: 30px; /* 移动端增加图标下边距 */
  }
  
  .platform-icon {
    width: 56px;
    height: 56px;
  }
  
  .platform-icon-img {
    width: 60%;
    height: 60%;
  }
  
  .cta-button {
    padding: 14px 30px;
    font-size: 1.2rem;
    min-width: 200px;
  }
}

@media (max-width: 640px) {
  .main-title {
    font-size: 2rem;
    margin-bottom: 14px;
  }
  
  .subtitle {
    font-size: 1.1rem;
    margin-bottom: 26px;
  }
  
  .platform-icons {
    gap: 10px;
    margin-bottom: 26px;
  }
  
  .platform-icon {
    width: 52px;
    height: 52px;
  }
  
  .cta-button {
    padding: 12px 28px;
    font-size: 1.1rem;
  }
}

@media (max-width: 480px) {
  .content-wrapper {
    padding: 0 10px;
    padding-top: 12px;
    padding-bottom: 12px;
  }
  
  .main-title {
    font-size: 1.8rem;
    margin-bottom: 12px;
    line-height: 1.3;
  }
  
  .subtitle {
    font-size: 1rem;
    margin-bottom: 24px;
    line-height: 1.4;
  }
  
  .platform-icons {
    gap: 8px;
    margin-bottom: 24px;
  }
  
  .platform-icon {
    width: 48px;
    height: 48px;
  }
  
  .platform-icon-img {
    width: 55%;
    height: 55%;
  }
  
  .cta-button {
    padding: 10px 24px;
    font-size: 1rem;
    min-width: 180px;
  }
}

@media (max-width: 360px) {
  .platform-icons {
    gap: 6px;
  }
  
  .platform-icon {
    width: 44px;
    height: 44px;
  }
  
  .main-title {
    font-size: 1.6rem;
    margin-bottom: 10px;
  }
  
  .subtitle {
    font-size: 0.95rem;
    margin-bottom: 20px;
  }
  
  .cta-button {
    padding: 8px 20px;
    font-size: 0.95rem;
    min-width: 160px;
  }
}
</style>