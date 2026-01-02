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
    answer: 'Monthly limit refers to the maximum amount of resources or services you can use within a billing cycle. It helps manage usage and prevents unexpected charges.'
  },
  {
    id: 2,
    question: 'Am I allowed to advertise blackhat on your accounts?',
    answer: 'No, we do not allow any blackhat advertising on our platform. All advertising must comply with our terms of service and follow ethical marketing practices.'
  },
  {
    id: 3,
    question: 'Can I upgrade in the middle of my plan?',
    answer: 'Yes, you can upgrade your plan at any time. The new plan will take effect immediately, and you will be charged the prorated difference for the remaining billing period.'
  },
  {
    id: 4,
    question: 'How can I top up?',
    answer: 'You can top up your account balance by going to the Billing section in your dashboard. We accept credit cards, PayPal, and bank transfers.'
  },
  {
    id: 5,
    question: 'How much for extra ad accounts?',
    answer: 'Additional ad accounts are available at $50 per account per month. You can add extra accounts from the Account Settings page.'
  },
  {
    id: 6,
    question: 'Where do I get my setup from?',
    answer: 'After purchasing a plan, you will receive an email with setup instructions. You can also find setup guides in the Documentation section of your dashboard.'
  }
])
</script>

<style scoped>
.faq-container {
  min-height: 100vh;
  background-color: #000;
  color: #fff;
  padding: 40px 20px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
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

/* 修改主标题字体 */
.faq-title {
  font-size: 35px;
  font-weight: 700;
  line-height: 1.2;
  margin-bottom: 20px;
  color: #fff;
  text-align: left;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; /* 使用更现代的字体 */
  letter-spacing: -0.5px; /* 微调字母间距 */
}

.faq-subtitle {
  font-size: 18px;
  color: #aaa;
  line-height: 1.6;
  margin-bottom: 0;
  text-align: left;
  font-weight: 400;
}

/* 移除下划线，修改为普通链接样式 */
.contact-link {
  color: #fff;
  text-decoration: none; /* 移除下划线 */
  border-bottom: none; /* 移除边框下划线 */
  padding-bottom: 0; /* 移除padding */
  transition: opacity 0.3s ease;
  display: inline-block;
  font-weight: 500; /* 稍微加粗 */
  margin-left: 4px; /* 添加一点间距 */
}

.contact-link:hover {
  opacity: 0.8;
  text-decoration: none; /* 确保悬停时也没有下划线 */
}

.faq-right {
  flex: 1.5;
}

/* 移动端样式 - 默认隐藏 */
.faq-mobile {
  display: none;
}

/* Element Plus 组件样式覆盖 - 确保左对齐 */
:deep(.el-collapse) {
  border: none;
  background: transparent;
  text-align: left;
}

:deep(.el-collapse-item) {
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  background: transparent;
  margin-bottom: 0;
  text-align: left;
}

/* 问题标题左对齐 */
:deep(.el-collapse-item__header) {
  height: auto;
  min-height: 60px;
  line-height: 1.4;
  font-size: 18px;
  background: transparent;
  color: #fff;
  padding: 20px 0;
  border: none;
  display: flex;
  align-items: center;
  cursor: pointer;
  transition: all 0.3s ease;
  text-align: left;
  justify-content: flex-start; /* 确保内容左对齐 */
  font-weight: 500; /* 问题文字中等粗细 */
}

:deep(.el-collapse-item__header:hover) {
  color: #ddd;
}

:deep(.el-collapse-item__arrow) {
  color: #fff;
  font-size: 20px;
  font-weight: 200;
  margin-right: 0;
  margin-left: auto; /* 箭头靠右，文字在左 */
  transform: rotate(90deg);
  transition: transform 0.3s ease;
  flex-shrink: 0; /* 防止箭头被压缩 */
}

:deep(.el-collapse-item__arrow.is-active) {
  transform: rotate(-90deg);
}

:deep(.el-collapse-item__wrap) {
  background: transparent;
  border: none;
  padding-bottom: 20px;
  text-align: left;
}

:deep(.el-collapse-item__content) {
  padding: 0;
  font-size: 16px;
  line-height: 1.6;
  color: #aaa;
  background: transparent;
  text-align: left;
  font-weight: 400;
}

/* 问题标题确保左对齐 */
.question-title {
  flex: 1;
  padding-right: 20px;
  font-weight: 500;
  text-align: left;
  width: 100%;
}

.answer-content {
  animation: fadeIn 0.3s ease;
  text-align: left;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* 响应式设计 */
@media (max-width: 768px) {
  .faq-container {
    padding: 20px 16px;
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
    font-size: 32px;
    margin-bottom: 16px;
    text-align: left;
    font-weight: 700;
    letter-spacing: -0.3px;
  }
  
  .faq-subtitle {
    font-size: 16px;
    margin-bottom: 30px;
    text-align: left;
  }
  
  /* 移动端问题列表左对齐优化 */
  :deep(.el-collapse-item__header) {
    font-size: 16px;
    padding: 16px 0;
    min-height: 50px;
    text-align: left;
    display: flex;
    justify-content: flex-start;
  }
  
  :deep(.el-collapse-item__content) {
    font-size: 14px;
    text-align: left;
  }
  
  /* 移动端箭头位置调整 */
  :deep(.el-collapse-item__arrow) {
    margin-left: auto;
    flex-shrink: 0;
  }
  
  .faq-right {
    width: 100%;
  }
  
  /* 移动端确保标题和副标题左对齐 */
  .faq-mobile .faq-title,
  .faq-mobile .faq-subtitle {
    text-align: left;
  }
  
  /* 移动端移除下划线 */
  .contact-link {
    text-decoration: none;
    border-bottom: none;
  }
}

/* 中等屏幕适配 */
@media (min-width: 769px) and (max-width: 1024px) {
  .faq-desktop {
    gap: 40px;
  }
  
  .faq-title {
    font-size: 36px;
    text-align: left;
    font-weight: 700;
  }
  
  .faq-subtitle {
    font-size: 16px;
    text-align: left;
  }
  
  /* 确保在中等屏幕上也左对齐 */
  .faq-left {
    text-align: left;
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
}
</style>