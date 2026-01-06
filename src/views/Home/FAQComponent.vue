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
            href="https://api.whatsapp.com/send?phone=8618603352371&text=hello" 
            target="_blank"
            class="social-button whatsapp-button"
          >
            <span class="button-text">WhatsApp</span>
            <!-- 使用img标签，不需要filter -->
            <img :src="whatsappIcon" class="whatsapp-icon-img" alt="WhatsApp" />
          </a>
          <a 
            href="https://t.me/luluyanyan2002" 
            target="_blank"
            class="social-button telegram-button"
          >
            <span class="button-text">Telegram</span>
            <span class="button-icon telegram-icon"></span>
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
          href="https://api.whatsapp.com/send?phone=8618603352371&text=hello" 
          target="_blank"
          class="social-button whatsapp-button"
        >
          <span class="button-text">WhatsApp</span>
          <img :src="whatsappIcon" class="whatsapp-icon-img" alt="WhatsApp" />
        </a>
        <a 
          href="https://t.me/luluyanyan2002" 
          target="_blank"
          class="social-button telegram-button"
        >
          <span class="button-text">Telegram</span>
          <span class="button-icon telegram-icon"></span>
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
import whatsapp from '@/assets/images/whatsapp.png'

// 当前展开的问题
const activeNames = ref([])

// WhatsApp图标 - 使用图片链接
const whatsappIcon = whatsapp

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
    question: 'How much does it cost to work with you?',
    answer: 'The pricing for our Agency Ad Accounts varies across different advertising platforms. Our pricing model involves a fixed monthly fee plus a percentage on each top-up. Feel free to contact us, and we\'ll work together to find the perfect plan for your business.'
  },
  {
    id: 5,
    question: 'Do you work with businesses of all sizes?',
    answer: 'Yes, we work with businesses of all sizes, from small startups to large corporations. Our services are customized based on the specific needs and goals of each client.'
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

/* 修改按钮组样式 - 根据图片样式 */
.button-group {
  display: flex;
  flex-direction: column;
  gap: 15px;
  margin-top: 30px;
  text-align: left;
  width: 100%;
  max-width: 280px;
}

.social-button {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 16px 24px;
  border-radius: 50px;
  font-size: 16px;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  cursor: pointer;
  border: none;
  height: 56px;
  min-height: 56px;
  text-align: center;
  line-height: 1;
  position: relative;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  width: 100%;
}

.social-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
}

.social-button:active {
  transform: translateY(0);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

/* WhatsApp按钮 - 绿色背景，白色文字 */
.whatsapp-button {
  background-color: #25D366;
  color: white;
}

.whatsapp-button:hover {
  background-color: #1ebe5d;
  box-shadow: 0 8px 20px rgba(37, 211, 102, 0.3);
}

/* Telegram按钮 - 浅蓝色背景，白色文字 */
.telegram-button {
  background-color: #2AABEE;
  color: white;
}

.telegram-button:hover {
  background-color: #229ed9;
  box-shadow: 0 8px 20px rgba(42, 171, 238, 0.3);
}

/* 按钮文字样式 */
.button-text {
  font-weight: 600;
  letter-spacing: 0.3px;
  font-size: 16px;
  color: white;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

/* WhatsApp图片图标样式 - 移除filter */
.whatsapp-icon-img {
  width: 24px;
  height: 24px;
  object-fit: contain;
  margin-left: 12px;
  /* 如果图片是白色电话图标，就不需要filter */
}

/* Telegram SVG图标样式 */
.button-icon {
  width: 24px;
  height: 24px;
  display: block;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  opacity: 0.9;
  filter: brightness(0) invert(1);
  margin-left: 12px;
}

.telegram-icon {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='white'%3E%3Cpath d='M12 0a12 12 0 1 0 0 24 12 12 0 0 0 0-24zm5.894 8.221l-1.97 9.28c-.145.658-.537.818-1.084.509l-3-2.21-1.446 1.394c-.16.16-.295.295-.605.295l.213-3.053 5.56-5.022c.242-.213-.054-.333-.373-.12l-6.87 4.326-2.96-.924c-.643-.204-.656-.643.135-.953l11.57-4.458c.536-.196 1.006.128.832.949z'/%3E%3C/svg%3E");
}

/* 修改主标题 */
.faq-title {
  font-size: 32px;
  font-weight: 700;
  line-height: 1.2;
  margin-bottom: 20px;
  color: #000000;
  text-align: left;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  letter-spacing: -0.5px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  display: block;
  max-width: 100%;
}

.faq-subtitle {
  font-size: 18px;
  color: #666666;
  line-height: 1.6;
  margin-bottom: 0;
  text-align: left;
  font-weight: 400;
  margin-top: 8px;
}

.faq-right {
  flex: 1.5;
}

/* 移动端样式 - 默认隐藏 */
.faq-mobile {
  display: none;
}

/* Element Plus 组件样式覆盖 */
:deep(.el-collapse) {
  border: none;
  background: transparent;
  text-align: left;
}

:deep(.el-collapse-item) {
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  background: #ffffff;
  margin-bottom: 16px;
  text-align: left;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
  transition: all 0.3s ease;
  overflow: hidden;
}

:deep(.el-collapse-item:hover) {
  border-color: #d1d5db;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  transform: translateY(-2px);
}

:deep(.el-collapse-item.is-active) {
  border-color: #10b981;
  box-shadow: 0 4px 12px rgba(16, 185, 129, 0.15);
}

:deep(.el-collapse-item__header) {
  height: auto;
  min-height: 72px;
  line-height: 1.4;
  font-size: 18px;
  background: transparent;
  color: #1f2937;
  padding: 20px 24px;
  border: none;
  display: flex;
  align-items: center;
  cursor: pointer;
  transition: all 0.3s ease;
  text-align: left;
  justify-content: flex-start;
  font-weight: 600;
  border-radius: 12px 12px 0 0;
}

:deep(.el-collapse-item__header:hover) {
  color: #111827;
  background-color: #f9fafb;
  padding-left: 24px;
  padding-right: 24px;
}

:deep(.el-collapse-item__arrow) {
  color: #6b7280;
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
  color: #10b981;
  background: rgba(16, 185, 129, 0.1);
}

:deep(.el-collapse-item__wrap) {
  background: transparent;
  border: none;
  text-align: left;
  border-top: 1px solid #f3f4f6;
}

:deep(.el-collapse-item__content) {
  padding: 0 24px 20px;
  font-size: 16px;
  line-height: 1.6;
  color: #4b5563;
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

.question-title {
  flex: 1;
  padding-right: 20px;
  font-weight: 600;
  text-align: left;
  width: 100%;
  color: #1f2937;
  font-size: 16px;
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
  
  /* 移动端标题字体调整 */
  .faq-title {
    font-size: 24px;
    margin-bottom: 16px;
    text-align: left;
    font-weight: 700;
    letter-spacing: -0.3px;
    white-space: normal;
    line-height: 1.3;
  }
  
  .faq-subtitle {
    font-size: 16px;
    margin-bottom: 30px;
    text-align: left;
    color: #666666;
  }
  
  /* 移动端按钮样式优化 */
  .mobile-button-group {
    display: flex;
    flex-direction: column;
    gap: 12px;
    margin-top: 20px;
    margin-bottom: 30px;
    width: 100%;
  }
  
  .mobile-button-group .social-button {
    width: 100%;
    font-size: 15px;
    padding: 16px 20px;
    height: 52px;
    min-height: 52px;
    border-radius: 50px;
  }
  
  .mobile-button-group .button-text {
    font-size: 15px;
  }
  
  .mobile-button-group .whatsapp-icon-img,
  .mobile-button-group .button-icon {
    width: 20px;
    height: 20px;
    margin-left: 10px;
  }
  
  /* 移动端FAQ边框样式优化 */
  :deep(.el-collapse-item) {
    border-radius: 10px;
    margin-bottom: 12px;
  }
  
  :deep(.el-collapse-item__header) {
    font-size: 16px;
    padding: 16px 20px;
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
}

/* 小屏幕手机适配 */
@media (max-width: 480px) {
  .faq-title {
    font-size: 20px;
    line-height: 1.2;
  }
  
  .faq-subtitle {
    font-size: 15px;
  }
  
  .mobile-button-group {
    gap: 10px;
  }
  
  .mobile-button-group .social-button {
    padding: 14px 16px;
    height: 48px;
    min-height: 48px;
    font-size: 14px;
  }
  
  .mobile-button-group .button-text {
    font-size: 14px;
  }
  
  .mobile-button-group .whatsapp-icon-img,
  .mobile-button-group .button-icon {
    width: 18px;
    height: 18px;
    margin-left: 8px;
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

/* 平板设备适配 */
@media (min-width: 769px) and (max-width: 1024px) {
  .faq-desktop {
    gap: 40px;
  }
  
  .faq-title {
    font-size: 28px;
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
    padding: 14px 20px;
    font-size: 15px;
    height: 52px;
  }
  
  .button-text {
    font-size: 15px;
  }
  
  .whatsapp-icon-img,
  .button-icon {
    width: 20px;
    height: 20px;
    margin-left: 10px;
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
    font-size: 36px;
    white-space: nowrap;
    overflow: visible;
  }
  
  .faq-subtitle {
    font-size: 20px;
  }
  
  .social-button {
    font-size: 16px;
    padding: 18px 28px;
    height: 60px;
  }
  
  .button-text {
    font-size: 16px;
  }
  
  .whatsapp-icon-img,
  .button-icon {
    width: 24px;
    height: 24px;
    margin-left: 12px;
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