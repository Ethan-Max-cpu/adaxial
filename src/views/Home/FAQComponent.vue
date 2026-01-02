<template>
  <div class="faq-container">
    <!-- 桌面端布局 -->
    <div class="faq-desktop">
      <div class="faq-left">
        <b class="faq-title">Frequently asked questions</b>
        
        <p class="faq-subtitle">
          <br>Don't see the answer you're looking for?<br>
          Get in touch.
        </p>
        
        <!-- 新增按钮区域 -->
        <div class="button-group">
          <a 
            href="https://t.me/luluyanyan2002" 
            target="_blank"
            class="social-button telegram-button"
          >
            Join telegram
          </a>
          <a 
            href="https://api.whatsapp.com/send?phone=8618603352371&text=hello" 
            target="_blank"
            class="social-button whatsapp-button"
          >
            Join Whatsapp
          </a>
        </div>
      </div>
      
      <div class="faq-right">
        <el-collapse v-model="activeNames" accordion>
          <el-collapse-item 
            v-for="item in faqItems" 
            :key="item.id" 
            :name="item.id"
            :title="item.question"
            class="faq-item"
          >
            <template #title>
              <div class="question-title">{{ item.question }}</div>
            </template>
            <div class="answer-content">{{ item.answer }}</div>
          </el-collapse-item>
        </el-collapse>
      </div>
    </div>

    <!-- 移动端布局 -->
    <div class="faq-mobile">
      <h1 class="faq-title">Frequently asked questions</h1>
      <p class="faq-subtitle">
        Don't see the answer you're looking for?Get in touch.
      </p>
      
      <!-- 移动端按钮区域 -->
      <div class="button-group mobile-button-group">
        <a 
          href="https://t.me/luluyanyan2002" 
          target="_blank"
          class="social-button telegram-button"
        >
          Join telegram
        </a>
        <a 
          href="https://api.whatsapp.com/send?phone=8618603352371&text=hello" 
          target="_blank"
          class="social-button whatsapp-button"
        >
          Join Whatsapp
        </a>
      </div>
      
      <el-collapse v-model="activeNames" accordion>
        <el-collapse-item 
          v-for="item in faqItems" 
          :key="item.id" 
          :name="item.id"
          :title="item.question"
          class="faq-item"
        >
          <template #title>
            <div class="question-title">{{ item.question }}</div>
          </template>
          <div class="answer-content">{{ item.answer }}</div>
        </el-collapse-item>
      </el-collapse>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { ElCollapse, ElCollapseItem } from 'element-plus'

// 当前展开的问题
const activeNames = ref([])

// FAQ数据
const faqItems = ref([
  {
    id: 1,
    question: 'What does the monthly limit mean?',
    answer: 'We created the Bronze & Gold plans to offer more affordable options for starters. Once you pass the monthly limit in spend -- you\'ll have to upgrade.'
  },
  {
    id: 2,
    question: 'Can I upgrade in the middle of my plan?',
    answer: 'Yes - we will discount the remaining days from your plan for the upgrade. You won\'t pay extra for the upgrade!'
  },
  {
    id: 3,
    question: 'How can I top up?',
    answer: 'You can top up via Bank (Wire/ACH, no spend fees) or Crypto (+1% fee). We\'ll add your top up to the ad account as soon as it arrives.'
  },
  {
    id: 4,
    question: 'How much for extra ad accounts?',
    answer: 'We charge +$30/month per each additional ad account.\nThis means 1 extra ad account = +$30.\nA 2nd extra ad account = $30 + $30 = +$60\nA 3rd extra ad account = $100 + $30 = +$130\nA 4th extra account = $150 + $30 = +$180 etc. etc.'
  },
  {
    id: 5,
    question: 'Where do I get my setup from?',
    answer: 'We partnered up with alphavault.store - our preferred partner for assets. Each client is eligible for 1x FB setup (1x Account + 1x BM + 1x Page) upon purchase, and afterwards a monthly credit of $50 for assets.'
  }
])
</script>

<style scoped>
.faq-container {
  background-color: #ffffff;
  color: #000000;
  padding: 60px 20px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
  min-height: auto;
}

/* 桌面端样式 */
.faq-desktop {
  display: flex;
  max-width: 1200px;
  margin: 0 auto;
  gap: 80px;
}

.faq-left {
  flex: 1;
  position: sticky;
  top: 40px;
  height: fit-content;
}

/* 新增按钮组样式 */
.button-group {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-top: 30px;
  text-align: left;
}

.social-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 12px 24px;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s ease;
  cursor: pointer;
  border: 2px solid transparent;
  min-height: 50px;
  text-align: center;
  line-height: 1.4;
}

.telegram-button {
  background-color: #f8f9fa;
  color: #333;
  border-color: #8b5cf6;
  border-width: 1px;
}

.telegram-button:hover {
  background-color: #ffffff;
  transform: translateY(-2px);
  box-shadow: 0 5px 20px rgba(139, 92, 246, 0.2);
  border-color: #8b5cf6;
  border-width: 1px;
}

.whatsapp-button {
  background-color: #f8f9fa;
  color: #333;
  border-color: #8b5cf6;
  border-width: 1px;
}

.whatsapp-button:hover {
  background-color: #ffffff;
  transform: translateY(-2px);
  box-shadow: 0 5px 20px rgba(139, 92, 246, 0.2);
  border-color: #8b5cf6;
  border-width: 1px;
}

/* 修改主标题 - 确保在一行内展示 */
.faq-title {
  font-size: 32px; /* 调整字体大小确保在一行内 */
  font-weight: 700;
  line-height: 1.2;
  margin-bottom: 20px;
  color: #000000;
  text-align: left;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  letter-spacing: -0.5px;
  white-space: nowrap; /* 强制在一行内显示 */
  overflow: hidden; /* 隐藏溢出部分 */
  text-overflow: ellipsis; /* 如果文本太长显示省略号 */
  display: block;
  max-width: 100%; /* 确保不超过容器宽度 */
}

.faq-subtitle {
  font-size: 18px;
  color: #666666;
  line-height: 1.6;
  margin-bottom: 0;
  text-align: left;
  font-weight: 400;
  margin-top: 8px; /* 增加与标题的距离 */
}

.contact-link {
  color: #333333;
  text-decoration: none;
  border-bottom: none;
  padding-bottom: 0;
  transition: opacity 0.3s ease;
  display: inline-block;
  font-weight: 500;
  margin-left: 4px;
}

.contact-link:hover {
  opacity: 0.8;
  text-decoration: none;
}

.faq-right {
  flex: 1.5;
}

/* 移动端样式 - 默认隐藏 */
.faq-mobile {
  display: none;
}

/* Element Plus 组件样式覆盖 - 要求1: 添加美观的灰色边框 */
:deep(.el-collapse) {
  border: none;
  background: transparent;
  text-align: left;
}

/* 为每个FAQ项目添加圆角灰色边框 */
:deep(.el-collapse-item) {
  border: 1px solid #e5e7eb; /* 浅灰色边框 */
  border-radius: 12px; /* 圆角边框 */
  background: #ffffff;
  margin-bottom: 16px; /* 增加间距 */
  text-align: left;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05); /* 轻微阴影增加层次感 */
  transition: all 0.3s ease;
  overflow: hidden; /* 确保圆角效果 */
}

/* 悬停效果 */
:deep(.el-collapse-item:hover) {
  border-color: #d1d5db; /* 悬停时边框颜色变深 */
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  transform: translateY(-2px);
}

/* 激活状态 */
:deep(.el-collapse-item.is-active) {
  border-color: #8b5cf6; /* 激活时边框变为紫色 */
  box-shadow: 0 4px 12px rgba(139, 92, 246, 0.15);
}

/* 问题标题样式优化 */
:deep(.el-collapse-item__header) {
  height: auto;
  min-height: 72px; /* 增加高度 */
  line-height: 1.4;
  font-size: 18px;
  background: transparent;
  color: #1f2937; /* 深灰色文字 */
  padding: 20px 24px; /* 增加内边距 */
  border: none;
  display: flex;
  align-items: center;
  cursor: pointer;
  transition: all 0.3s ease;
  text-align: left;
  justify-content: flex-start;
  font-weight: 600; /* 加粗字体 */
  border-radius: 12px 12px 0 0; /* 顶部圆角 */
}

:deep(.el-collapse-item__header:hover) {
  color: #111827; /* 更深的灰色 */
  background-color: #f9fafb; /* 悬停背景色 */
  padding-left: 24px;
  padding-right: 24px;
}

:deep(.el-collapse-item__arrow) {
  color: #6b7280; /* 中灰色箭头 */
  font-size: 20px;
  font-weight: 200;
  margin-right: 0;
  margin-left: auto;
  transform: rotate(90deg);
  transition: all 0.3s ease;
  flex-shrink: 0;
  padding: 4px;
  border-radius: 50%;
  background: #f3f4f6;
  width: 28px;
  height: 28px;
  display: flex;
  align-items: center;
  justify-content: center;
}

:deep(.el-collapse-item__arrow:hover) {
  background: #e5e7eb;
  color: #4b5563;
}

:deep(.el-collapse-item__arrow.is-active) {
  transform: rotate(-90deg);
  color: #8b5cf6; /* 激活时箭头变为紫色 */
  background: rgba(139, 92, 246, 0.1);
}

:deep(.el-collapse-item__wrap) {
  background: transparent;
  border: none;
  text-align: left;
  border-top: 1px solid #f3f4f6; /* 内容区域顶部边框 */
}

:deep(.el-collapse-item__content) {
  padding: 0 24px 20px; /* 增加左右和下边距 */
  font-size: 16px;
  line-height: 1.6;
  color: #4b5563; /* 中灰色文字 */
  background: transparent;
  text-align: left;
  font-weight: 400;
  animation: contentSlideDown 0.3s ease-out;
}

@keyframes contentSlideDown {
  from {
    opacity: 0;
    max-height: 0;
  }
  to {
    opacity: 1;
    max-height: 500px;
  }
}

/* 问题标题确保左对齐 */
.question-title {
  flex: 1;
  padding-right: 20px;
  font-weight: 600; /* 加粗 */
  text-align: left;
  width: 100%;
  color: #1f2937;
  font-size: 16px; /* 稍微缩小字体 */
  line-height: 1.5;
}

.answer-content {
  animation: fadeIn 0.3s ease;
  text-align: left;
  white-space: pre-line;
  color: #4b5563;
  line-height: 1.7;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-8px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* 响应式设计 - 移动端适配 */
@media (max-width: 768px) {
  .faq-container {
    padding: 30px 16px;
  }
  
  /* 隐藏桌面端布局 */
  .faq-desktop {
    display: none;
  }
  
  /* 显示移动端布局 */
  .faq-mobile {
    display: block;
  }
  
  /* 移动端标题字体调整 - 确保在一行内 */
  .faq-title {
    font-size: 24px; /* 移动端适当减小字体 */
    margin-bottom: 16px;
    text-align: left;
    font-weight: 700;
    letter-spacing: -0.3px;
    white-space: normal; /* 移动端允许换行 */
    line-height: 1.3; /* 调整行高 */
  }
  
  .faq-subtitle {
    font-size: 16px;
    margin-bottom: 30px;
    text-align: left;
    color: #666666;
  }
  
  /* 移动端按钮样式 */
  .mobile-button-group {
    margin-top: 20px;
    margin-bottom: 30px;
  }
  
  .mobile-button-group .social-button {
    width: 100%;
    font-size: 15px;
    padding: 14px 20px;
  }
  
  /* 移动端FAQ边框样式优化 */
  :deep(.el-collapse-item) {
    border-radius: 10px; /* 稍微小的圆角 */
    margin-bottom: 12px;
  }
  
  /* 移动端问题列表左对齐优化 */
  :deep(.el-collapse-item__header) {
    font-size: 16px;
    padding: 16px 20px; /* 移动端适当减小内边距 */
    min-height: 60px;
    text-align: left;
    display: flex;
    justify-content: flex-start;
    border-radius: 10px 10px 0 0;
  }
  
  :deep(.el-collapse-item__header:hover) {
    padding-left: 20px;
    padding-right: 20px;
  }
  
  :deep(.el-collapse-item__content) {
    font-size: 14px;
    text-align: left;
    padding: 0 20px 16px;
  }
  
  /* 移动端箭头样式调整 */
  :deep(.el-collapse-item__arrow) {
    width: 24px;
    height: 24px;
    font-size: 18px;
  }
  
  .faq-right {
    width: 100%;
  }
  
  /* 移动端确保标题和副标题左对齐 */
  .faq-mobile .faq-title,
  .faq-mobile .faq-subtitle {
    text-align: left;
  }
  
  .contact-link {
    text-decoration: none;
    border-bottom: none;
  }
}

/* 小屏幕手机适配 */
@media (max-width: 480px) {
  .faq-title {
    font-size: 20px; /* 在小屏幕上进一步减小字体 */
    line-height: 1.2;
  }
  
  .faq-subtitle {
    font-size: 15px;
  }
  
  .mobile-button-group .social-button {
    padding: 12px 16px;
    font-size: 14px;
  }
  
  :deep(.el-collapse-item) {
    border-radius: 8px;
    margin-bottom: 10px;
  }
  
  :deep(.el-collapse-item__header) {
    font-size: 15px;
    padding: 14px 16px;
    min-height: 56px;
    border-radius: 8px 8px 0 0;
  }
  
  :deep(.el-collapse-item__arrow) {
    width: 22px;
    height: 22px;
    font-size: 16px;
  }
  
  :deep(.el-collapse-item__content) {
    font-size: 13px;
    padding: 0 16px 14px;
  }
  
  .question-title {
    font-size: 15px;
  }
}

/* 平板设备适配 - 调整标题以适合一行 */
@media (min-width: 769px) and (max-width: 1024px) {
  .faq-desktop {
    gap: 40px;
  }
  
  .faq-title {
    font-size: 28px; /* 平板设备上调整字体大小 */
    text-align: left;
    font-weight: 700;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  
  .faq-subtitle {
    font-size: 16px;
    text-align: left;
  }
  
  /* 确保在中等屏幕上也左对齐 */
  .faq-left {
    text-align: left;
  }
  
  /* 中等屏幕按钮调整 */
  .social-button {
    padding: 10px 20px;
    font-size: 15px;
  }
  
  /* 平板端折叠面板调整 */
  :deep(.el-collapse-item) {
    border-radius: 10px;
  }
  
  :deep(.el-collapse-item__header) {
    font-size: 16px;
    min-height: 60px;
    padding: 18px 20px;
  }
  
  :deep(.el-collapse-item__content) {
    font-size: 15px;
    padding: 0 20px 18px;
  }
}

/* 桌面端左对齐优化 */
@media (min-width: 1025px) {
  .faq-left {
    text-align: left;
  }
  
  /* 确保整个右栏内容左对齐 */
  .faq-right {
    text-align: left;
  }
  
  /* 桌面端悬停效果优化 */
  :deep(.el-collapse-item__header:hover) {
    padding-left: 24px;
    padding-right: 24px;
  }
}

/* 超大屏幕适配 */
@media (min-width: 1440px) {
  .faq-container {
    padding: 80px 20px;
  }
  
  .faq-title {
    font-size: 36px; /* 超大屏幕上适当增大字体 */
    white-space: nowrap;
    overflow: visible; /* 超大屏幕上不需要隐藏 */
  }
  
  .faq-subtitle {
    font-size: 20px;
  }
  
  .social-button {
    font-size: 18px;
    padding: 15px 30px;
  }
  
  /* 大屏幕FAQ边框优化 */
  :deep(.el-collapse-item) {
    border-radius: 16px;
    margin-bottom: 20px;
  }
  
  :deep(.el-collapse-item__header) {
    min-height: 80px;
    padding: 24px 32px;
    font-size: 18px;
    border-radius: 16px 16px 0 0;
  }
  
  :deep(.el-collapse-item__content) {
    padding: 0 32px 24px;
    font-size: 16px;
  }
  
  .question-title {
    font-size: 18px;
  }
}
</style>