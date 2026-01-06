<template>
  <div class="promo-container">
    <!-- 第一部分：加粗标题 -->
    <h1 class="promo-title">Agency accounts for all platforms</h1>
    
    <!-- 第二部分：正文 -->
    <p class="promo-subtitle">Fastest turnarounds and best rates in the industry</p>
    
    <!-- 第三部分：图标展示 -->
    <div class="icons-container">
      <div 
        v-for="(icon, index) in socialIcons" 
        :key="index" 
        class="icon-item"
        :style="{ backgroundColor: icon.color }"
      >
        <span class="icon-text">{{ icon.text }}</span>
      </div>
    </div>
    
    <!-- 第四部分：按钮 -->
    <el-button 
      class="action-button" 
      type="primary" 
      @click="handleClick"
    >
      Get Started Now!
    </el-button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { ElButton } from 'element-plus'

// 图标数据 - 按照图片中的样式
const socialIcons = ref([
  { text: 'f', color: '#1877F2' }, // Facebook
  { text: 'in', color: '#0A66C2' }, // LinkedIn
  { text: 'tw', color: '#1DA1F2' }, // Twitter
  { text: 'ig', color: '#E4405F' }, // Instagram
  { text: 'yt', color: '#FF0000' }, // YouTube
  { text: 'tt', color: '#000000' }, // TikTok
])

// 点击按钮的处理函数
const handleClick = () => {
  // 这里替换为您需要的跳转链接
  window.open('https://your-link-here.com', '_blank')
}
</script>

<style scoped>
.promo-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 40px 20px;
  background-color: white;
  min-height: 100vh;
  text-align: center;
  box-sizing: border-box;
}

/* 第一部分：加粗标题 */
.promo-title {
  font-size: 2.5rem;
  font-weight: 900;
  color: #000000;
  margin: 0 0 20px 0;
  line-height: 1.2;
  max-width: 600px;
}

/* 第二部分：正文 */
.promo-subtitle {
  font-size: 1.2rem;
  color: #666666;
  margin: 0 0 40px 0;
  line-height: 1.5;
  max-width: 400px;
}

/* 第三部分：图标容器 */
.icons-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 15px;
  margin: 0 0 40px 0;
  max-width: 500px;
}

/* 单个图标样式 */
.icon-item {
  width: 60px;
  height: 60px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  font-size: 1.5rem;
  color: white;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.icon-item:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

/* 图标内的文字 */
.icon-text {
  font-weight: 700;
  font-family: Arial, sans-serif;
}

/* 第四部分：按钮 */
.action-button {
  background-color: #10B981 !important;
  border-color: #10B981 !important;
  font-size: 1.2rem;
  font-weight: 600;
  padding: 15px 40px;
  border-radius: 8px;
  transition: all 0.3s ease;
  border: none;
  color: white;
}

.action-button:hover {
  background-color: #059669 !important;
  border-color: #059669 !important;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(16, 185, 129, 0.3);
}

/* 移动端适配 */
@media (max-width: 768px) {
  .promo-container {
    padding: 20px 15px;
  }
  
  .promo-title {
    font-size: 1.8rem;
    margin-bottom: 15px;
  }
  
  .promo-subtitle {
    font-size: 1rem;
    margin-bottom: 30px;
  }
  
  .icons-container {
    gap: 10px;
    margin-bottom: 30px;
  }
  
  .icon-item {
    width: 50px;
    height: 50px;
    font-size: 1.2rem;
  }
  
  .action-button {
    font-size: 1rem;
    padding: 12px 30px;
  }
}

@media (max-width: 480px) {
  .promo-title {
    font-size: 1.5rem;
  }
  
  .promo-subtitle {
    font-size: 0.9rem;
  }
  
  .icons-container {
    gap: 8px;
  }
  
  .icon-item {
    width: 45px;
    height: 45px;
    font-size: 1rem;
  }
}
</style>