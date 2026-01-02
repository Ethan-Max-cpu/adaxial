<template>
  <div class="ad-revival-container">
    <!-- 标题部分 -->
    <div class="title-section">
      <h1 class="main-title">Why Adaxial?</h1>
    </div>

    <!-- 卡片容器 -->
    <div class="cards-container">
      <!-- 动态渲染卡片 -->
      <el-card
        v-for="(card, index) in cardData"
        :key="index"
        class="feature-card"
        shadow="hover"
      >
        <template #header>
          <div class="card-header">
            <h3 class="card-title">{{ card.title }}</h3>
          </div>
        </template>
        <div class="card-content">
          <p>{{ card.content }}</p>
        </div>
      </el-card>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { ElCard } from 'element-plus'

// 响应式卡片数据
const cardData = ref([
  { 
    title: 'Advertise Across Every Niche.', 
    content: 'Launch nearly any ad format on any advertising platform—no matter which industry you operate in. We’ve got tailored solutions for every business type, and every ad platform.' 
  },
  { 
    title: 'Keep Your Campaigns Live Uninterrupted.', 
    content: 'If your ad account gets suspended, we’ll replace it for you right away—so your advertising efforts keep running without a single pause.' 
  },
  { 
    title: 'Slash Your CPA & CPM Costs.', 
    content: 'Our whitelisted agency ad accounts have built a strong, long-standing reputation. This lets us secure CPA and CPM rates that are up to 50% lower.' 
  },
])

// 响应式屏幕宽度
const screenWidth = ref(window.innerWidth)

// 根据屏幕宽度计算要显示的卡片数量
const visibleCards = computed(() => {
  if (screenWidth.value < 768) {
    return 1 // 移动端显示1列
  } else if (screenWidth.value < 1024) {
    return 2 // 平板显示2列
  } else {
    return 3 // 桌面端显示3列
  }
})

// 监听窗口大小变化
const handleResize = () => {
  screenWidth.value = window.innerWidth
}

onMounted(() => {
  window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
  window.removeEventListener('resize', handleResize)
})
</script>

<style scoped>
.ad-revival-container {
  background-color: #ffffff; /* 改为白色背景 */
  color: #1f2937; /* 改为深灰色文字 */
  padding: 40px 5%; /* 左右留白，减少上下内边距 */
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
  box-sizing: border-box;
}

/* 标题样式 - 适配白色背景 */
.title-section {
  width: 100%;
  margin-bottom: 40px; /* 减少标题下边距 */
  text-align: center;
}

.main-title {
  font-size: clamp(2.5rem, 6vw, 3.5rem); /* 稍微减小最大字体 */
  font-weight: 700;
  margin: 0;
  line-height: 1.1;
  letter-spacing: -0.5px;
  color: #111827; /* 改为深灰色适配白色背景 */
  background: linear-gradient(90deg, #10b981, #059669); /* 添加绿色渐变 */
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  -webkit-text-fill-color: transparent;
}

/* 卡片容器 */
.cards-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); /* 稍微减小最小宽度 */
  gap: 20px; /* 减少卡片间距 */
  width: 100%;
  max-width: 1200px; /* 减小最大宽度 */
  margin: 0 auto;
}

/* 卡片样式 - 适配白色背景 */
.feature-card {
  background: linear-gradient(135deg, #f9fafb 0%, #f3f4f6 100%); /* 改为浅灰色渐变 */
  border: 1px solid rgba(209, 213, 219, 0.5); /* 改为浅灰色边框 */
  border-radius: 12px; /* 减小圆角 */
  color: #1f2937; /* 改为深灰色文字 */
  height: 100%;
  display: flex;
  flex-direction: column;
  transition: all 0.2s ease; /* 加快过渡动画 */
  overflow: hidden;
  padding: 20px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
}

.feature-card:hover {
  transform: translateY(-3px); /* 减小上移距离 */
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.12);
  border-color: rgba(16, 185, 129, 0.3); /* 悬停时绿色边框 */
  background: linear-gradient(135deg, #ffffff 0%, #f9fafb 100%); /* 悬停时更浅的背景 */
}

.feature-card :deep(.el-card__header) {
  background-color: transparent;
  border: none;
  padding: 0 0 15px 0; /* 减少内边距 */
}

.card-header {
  min-height: 60px; /* 减少最小高度 */
  display: flex;
  align-items: center;
  padding-bottom: 10px; /* 减少下内边距 */
  border-bottom: 1px solid rgba(209, 213, 219, 0.5); /* 改为浅灰色分隔线 */
}

.card-title {
  font-size: clamp(1.2rem, 2vw, 1.4rem); /* 减小字体大小 */
  font-weight: 600;
  margin: 0;
  line-height: 1.3;
  color: #111827; /* 改为深灰色 */
}

.feature-card :deep(.el-card__body) {
  padding: 0;
  flex: 1;
  display: flex;
  flex-direction: column;
}

.card-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  padding-top: 15px; /* 减少上内边距 */
}

.card-content p {
  font-size: clamp(0.95rem, 1.5vw, 1rem); /* 减小字体大小 */
  line-height: 1.6; /* 稍微减小行高 */
  margin: 0;
  opacity: 0.85;
  color: #4b5563; /* 改为中灰色 */
}

/* 移动端适配 */
@media (max-width: 768px) {
  .ad-revival-container {
    padding: 20px 5%; /* 减少移动端内边距 */
  }
  
  .title-section {
    margin-bottom: 25px; /* 减少移动端下边距 */
  }
  
  .cards-container {
    grid-template-columns: 1fr;
    gap: 15px; /* 减少移动端卡片间距 */
  }
  
  .feature-card {
    padding: 15px; /* 减少移动端内边距 */
  }
  
  .card-header {
    min-height: auto;
  }
  
  .main-title {
    font-size: clamp(2rem, 5vw, 2.5rem); /* 移动端字体调整 */
  }
}

/* 平板适配 */
@media (min-width: 769px) and (max-width: 1024px) {
  .ad-revival-container {
    padding: 30px 6%; /* 减小平板内边距 */
  }
  
  .cards-container {
    grid-template-columns: repeat(2, 1fr);
  }
  
  .main-title {
    font-size: clamp(2.2rem, 5vw, 3rem); /* 平板字体调整 */
  }
}

/* 桌面端适配 */
@media (min-width: 1025px) {
  .ad-revival-container {
    padding: 40px 8%; /* 减小桌面端内边距 */
  }
  
  .cards-container {
    grid-template-columns: repeat(3, 1fr);
  }
}

/* 小屏幕手机适配 */
@media (max-width: 480px) {
  .ad-revival-container {
    padding: 16px 4%; /* 进一步减小内边距 */
  }
  
  .title-section {
    margin-bottom: 20px;
  }
  
  .cards-container {
    gap: 12px;
  }
  
  .feature-card {
    padding: 12px;
  }
  
  .main-title {
    font-size: 1.8rem;
  }
  
  .card-title {
    font-size: 1.1rem;
  }
  
  .card-content p {
    font-size: 0.9rem;
    line-height: 1.5;
  }
}

/* 超大桌面适配 */
@media (min-width: 1400px) {
  .ad-revival-container {
    padding: 50px 10%; /* 保持相对较小的内边距 */
  }
  
  .cards-container {
    max-width: 1400px;
  }
  
  .feature-card {
    padding: 24px;
  }
}

/* 触摸设备优化 */
@media (hover: none) and (pointer: coarse) {
  .feature-card:hover {
    transform: none;
  }
  
  .feature-card:active {
    transform: translateY(-3px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.12);
  }
}
</style>