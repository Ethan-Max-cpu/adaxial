<template>
  <div class="steps-component">
    <!-- 标题部分 -->
    <div class="title-section">
      <div class="title-container">
        <h1>HOW IT WORKS</h1>
        <h2>Rent Ad Accounts in 3 Simple Steps</h2>
        <p class="subtitle">Getting started is fast, simple, and designed to keep your campaigns running smoothly—no stress, no bans.</p>
      </div>
    </div>

    <!-- 步骤内容区域 -->
    <div class="content-section">
      <div class="content-container">
        <!-- 左侧步骤列表 -->
        <div class="steps-list">
          <div 
            v-for="(step, index) in steps" 
            :key="index"
            :class="['step-item', { active: currentStepIndex === index }]"
            @click="setCurrentStep(index)"
          >
            <div class="step-number">Step {{ index + 1 }}</div>
            <div class="step-title">{{ step.title }}</div>
            <div class="step-desc">{{ step.description }}</div>
          </div>
        </div>

        <!-- 右侧内容展示区 - 添加动画过渡 -->
        <div class="step-content">
          <transition name="fade-slide" mode="out-in">
            <div class="content-display" :key="currentStepIndex">
              <!-- 添加 content-icon 容器 -->
              <div class="content-icon">
                <img 
                  :src="currentStep.icon" 
                  class="icon-img"
                  :alt="currentStep.title"
                >
              </div>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import icon01 from '@/assets/icons/icon-01.png';
import icon02 from '@/assets/icons/icon-02.png';
import icon03 from '@/assets/icons/icon-03.png';
export default {
  name: 'StepsComponent',
  data() {
    return {
      currentStepIndex: 0,
      steps: [
        {
          title: 'Share Your Business Details',
          description: 'Tell us about your website and business, and we will assess whether you are a suitable candidate for our advertising account.',
          icon: icon01
        },
        {
          title: 'Fund Your Account with Ease',
          description: 'After your application is approved, your agent account will be activated within 48 hours. You can top up your account using a credit card, cryptocurrency, or direct bank transfer.',
          icon: icon02
        },
        {
          title: 'Launch Ads Confidently',
          description: 'Start running ads immediately – your account is stable and reliable, designed for large-scale promotion, and enjoys comprehensive protection against account suspension.',
          icon: icon03
        }
      ]
    };
  },
  computed: {
    currentStep() {
      return this.steps[this.currentStepIndex];
    }
  },
  methods: {
    setCurrentStep(index) {
      this.currentStepIndex = index;
    }
  }
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
}

/* 主容器 - 背景改为白色 */
.steps-component {
  background: linear-gradient(135deg, #ffffff, #f8f9fa);
  min-height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  overflow-x: hidden; /* 防止水平滚动 */
}

/* 标题部分样式 - 调整内边距确保副标题在一行 */
.title-section {
  width: 100%;
  padding: 40px 0 30px;
  display: flex;
  justify-content: center;
  border-bottom: 1px solid #e5e7eb; /* 改为浅色边框适配白色背景 */
}

.title-container {
  width: 100%;
  max-width: 1400px; /* 增加最大宽度确保有足够空间 */
  padding: 0 100px; /* 增加左右内边距 */
  text-align: center;
}

/* 紫色字体缩小一号，适配白色背景 */
.title-section h1 {
  font-size: 2.0rem; /* 从 3rem 减小到 2.5rem */
  line-height: 1.1;
  margin-bottom: 12px;
  background: linear-gradient(90deg, #7d5fff, #4a6ee0);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  font-weight: 800;
  letter-spacing: 1.5px;
  text-transform: uppercase;
}

/* 深色字体大一号，适配白色背景 */
.title-section h2 {
  font-size: 3.0rem; /* 从 2.2rem 增大到 2.5rem */
  color: #1f2937; /* 改为深灰色适配白色背景 */
  margin-bottom: 15px;
  font-weight: 700;
  line-height: 1.2;
}

/* 关键优化：确保副标题在一行内显示，适配白色背景 */
.title-section .subtitle {
  font-size: 1.2rem; /* 减小字体大小 */
  color: #6b7280; /* 改为中灰色适配白色背景 */
  line-height: 1.4; /* 更紧凑的行高 */
  max-width: 100%; /* 移除最大宽度限制 */
  margin: 0 auto;
  font-weight: 400;
  white-space: nowrap; /* 防止换行 */
  overflow: hidden; /* 隐藏溢出 */
  text-overflow: ellipsis; /* 溢出时显示省略号 */
  padding: 0 20px; /* 添加内边距防止边缘截断 */
}

/* 内容区域样式 */
.content-section {
  width: 100%;
  display: flex;
  justify-content: center;
  flex: 1;
  padding: 30px 0;
}

.content-container {
  width: 100%;
  max-width: 1400px; /* 增加最大宽度以匹配标题区域 */
  padding: 0 100px; /* 增加左右内边距以匹配标题区域 */
  display: flex;
  gap: 50px;
  min-height: 400px;
}

/* 左侧步骤列表 - 适配白色背景 */
.steps-list {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 15px;
  min-width: 0;
}

.step-item {
  padding: 20px 25px;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border-left: 4px solid transparent;
  position: relative;
  overflow: hidden;
  background-color: rgba(248, 250, 252, 0.8); /* 改为浅色背景 */
  border: 1px solid #e5e7eb; /* 添加浅色边框 */
  width: 100%;
}

.step-item:hover {
  background-color: rgba(241, 245, 249, 0.9); /* 悬停时稍深的浅色 */
  transform: translateX(3px);
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.08);
  border-color: #d1d5db; /* 悬停时边框变深 */
}

.step-item.active {
  background-color: rgba(241, 245, 249, 0.9); /* 激活状态背景 */
  border-left: 4px solid #7d5fff;
  border-color: #7d5fff; /* 激活时整个边框也变紫色 */
  box-shadow: 0 5px 15px rgba(125, 95, 255, 0.15);
}

.step-number {
  font-size: 0.9rem;
  color: #7d5fff; /* 保持紫色 */
  font-weight: 700;
  margin-bottom: 8px;
  letter-spacing: 1.2px;
  text-transform: uppercase;
}

/* 步骤标题字体增大，适配白色背景 */
.step-title {
  font-size: 1.6rem; /* 从 1.5rem 增大到 1.6rem */
  font-weight: 700;
  margin-bottom: 8px;
  color: #1f2937; /* 改为深灰色 */
  line-height: 1.3;
}

.step-desc {
  font-size: 1.05rem;
  color: #4b5563; /* 改为中灰色 */
  line-height: 1.5;
  max-width: 100%;
  font-weight: 400;
}

/* 右侧内容展示区 */
.step-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  min-width: 0;
  position: relative;
  min-height: 380px;
}

.content-display {
  background: linear-gradient(135deg, #f1f5f9, #e2e8f0, #cbd5e1); /* 改为浅色渐变 */
  border-radius: 16px;
  padding: 30px 25px;
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  box-shadow: 0 15px 30px rgba(203, 213, 225, 0.3); /* 改为浅色阴影 */
  position: relative;
  overflow: hidden;
  height: 100%;
  width: 100%;
  border: 1px solid #e2e8f0; /* 添加边框 */
}

.content-display::before {
  content: '';
  position: absolute;
  top: -30%;
  right: -30%;
  width: 250px;
  height: 250px;
  background: rgba(125, 95, 255, 0.05); /* 改为紫色半透明 */
  border-radius: 50%;
  z-index: 0;
}

.content-display::after {
  content: '';
  position: absolute;
  bottom: -20%;
  left: -15%;
  width: 180px;
  height: 180px;
  background: rgba(74, 110, 224, 0.03); /* 改为蓝色半透明 */
  border-radius: 50%;
  z-index: 0;
}

/* 修改 .content-icon 样式，让它更小 */
.content-icon {
  width: 400px;  /* 从 100px 减小到 80px */
  height: 400px; /* 从 100px 减小到 80px */
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px; /* 减小下边距 */
  overflow: hidden;    /* 重要：让图片不溢出容器 */
  padding: 15px;      /* 减小内边距 */
  backdrop-filter: blur(4px);
  background: rgba(255, 255, 255, 0.6); /* 添加白色半透明背景 */
  border-radius: 12px; /* 添加圆角 */
  border: 1px solid rgba(255, 255, 255, 0.8); /* 添加白色边框 */
}

/* 修改 .icon-img 样式，让图片圆角并适合容器 */
.icon-img {
  width: 100%;        /* 占满容器宽度 */
  height: 100%;       /* 占满容器高度 */
  object-fit: contain; /* 保持图片比例 */
  border-radius: 8px; /* 添加圆角 */
  transition: transform 0.3s ease; /* 添加悬停效果 */
}

.content-title {
  font-size: 1.9rem;
  font-weight: 700;
  margin-bottom: 20px;
  color: #1f2937; /* 改为深灰色 */
  z-index: 1;
  line-height: 1.2;
}

.content-text {
  font-size: 1.1rem;
  line-height: 1.5;
  color: #4b5563; /* 改为中灰色 */
  max-width: 400px;
  margin-bottom: 15px;
  z-index: 1;
  font-weight: 400;
}

.user-info-section {
  margin-top: 25px;
  padding-top: 20px;
  border-top: 1px solid rgba(209, 213, 219, 0.3); /* 改为浅灰色 */
  width: 100%;
  max-width: 350px;
  z-index: 1;
}

.user-id {
  font-size: 1.4rem;
  font-weight: 700;
  color: #1f2937; /* 改为深灰色 */
  margin-bottom: 8px;
  letter-spacing: 1px;
}

.user-note {
  font-size: 1rem;
  color: #6b7280; /* 改为中灰色 */
  font-weight: 500;
}

/* 动画效果 */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

.fade-slide-enter-to,
.fade-slide-leave-from {
  opacity: 1;
  transform: translateY(0);
}

/* 移动端适配 - 响应式设计 */
@media (max-width: 1400px) {
  .title-container {
    padding: 0 80px;
  }
  
  .content-container {
    padding: 0 80px;
    gap: 40px;
  }
}

@media (max-width: 1200px) {
  .title-container {
    padding: 0 60px;
  }
  
  .content-container {
    padding: 0 60px;
    gap: 30px;
  }
  
  /* 移动端字体调整 */
  .title-section h1 {
    font-size: 2.2rem; /* 从 2.6rem 减小到 2.2rem */
  }
  
  .title-section h2 {
    font-size: 2.2rem; /* 从 1.9rem 增大到 2.2rem */
  }
  
  /* 在较小屏幕上允许副标题换行 */
  .title-section .subtitle {
    white-space: normal;
    max-width: 900px;
  }
  
  .step-title {
    font-size: 1.5rem; /* 从 1.4rem 增大到 1.5rem */
  }
  
  .content-icon {
    width: 350px;
    height: 350px;
  }
}

@media (max-width: 992px) {
  .title-container {
    padding: 0 40px;
  }
  
  .content-container {
    flex-direction: column;
    padding: 0 40px;
    gap: 30px;
  }
  
  .title-section {
    padding: 30px 0 20px;
  }
  
  .content-section {
    padding: 20px 0;
  }
  
  .step-item {
    padding: 18px 22px;
  }
  
  .content-display {
    min-height: 320px;
  }
  
  .title-section .subtitle {
    white-space: normal;
    line-height: 1.5;
  }
  
  .content-icon {
    width: 300px;
    height: 300px;
  }
}

@media (max-width: 768px) {
  .title-container {
    padding: 0 30px;
  }
  
  .content-container {
    padding: 0 30px;
  }
  
  .title-section {
    padding: 25px 0 15px;
  }
  
  .title-section h1 {
    font-size: 1.8rem; /* 从 2.2rem 减小到 1.8rem */
  }
  
  .title-section h2 {
    font-size: 2rem; /* 从 1.6rem 增大到 2rem */
  }
  
  .title-section .subtitle {
    font-size: 1.1rem;
    white-space: normal;
    line-height: 1.5;
  }
  
  .step-item {
    padding: 15px 18px;
  }
  
  .step-number {
    font-size: 0.85rem;
  }
  
  .step-title {
    font-size: 1.4rem; /* 从 1.2rem 增大到 1.4rem */
  }
  
  .step-desc {
    font-size: 1rem;
  }
  
  .content-display {
    padding: 25px 20px;
  }
  
  .content-icon {
    width: 250px;
    height: 250px;
    margin-bottom: 20px;
  }
  
  .content-title {
    font-size: 1.5rem;
  }
  
  .content-text {
    font-size: 1rem;
  }
  
  .user-id {
    font-size: 1.2rem;
  }
  
  .user-note {
    font-size: 0.9rem;
  }
}

@media (max-width: 576px) {
  .title-container {
    padding: 0 20px;
  }
  
  .content-container {
    padding: 0 20px;
  }
  
  .title-section {
    padding: 20px 0 12px;
  }
  
  .title-section h1 {
    font-size: 1.6rem; /* 从 1.8rem 减小到 1.6rem */
  }
  
  .title-section h2 {
    font-size: 1.8rem; /* 从 1.3rem 增大到 1.8rem */
  }
  
  .title-section .subtitle {
    font-size: 1rem;
    white-space: normal;
    line-height: 1.5;
  }
  
  .step-item {
    padding: 12px 15px;
  }
  
  .step-title {
    font-size: 1.3rem; /* 从 1.1rem 增大到 1.3rem */
  }
  
  .step-desc {
    font-size: 0.9rem;
  }
  
  .content-display {
    padding: 20px 15px;
  }
  
  .content-icon {
    width: 200px;
    height: 200px;
    margin-bottom: 15px;
  }
  
  .content-title {
    font-size: 1.3rem;
  }
  
  .content-text {
    font-size: 0.9rem;
  }
  
  .user-id {
    font-size: 1.1rem;
  }
}

/* 对于超大屏幕，确保副标题在一行内显示 */
@media (min-width: 1400px) {
  .title-section .subtitle {
    font-size: 1.25rem; /* 在大屏幕上稍微增加字体大小 */
  }
}

/* 对于超小屏幕，确保副标题正常显示 */
@media (max-width: 480px) {
  .title-section h1 {
    font-size: 1.4rem; /* 超小屏幕进一步缩小紫色字体 */
  }
  
  .title-section h2 {
    font-size: 1.6rem; /* 超小屏幕白色字体 */
  }
  
  .step-title {
    font-size: 1.2rem; /* 超小屏幕步骤标题 */
  }
  
  .content-icon {
    width: 180px;
    height: 180px;
  }
  
  .title-section .subtitle {
    white-space: normal;
    line-height: 1.5;
    text-overflow: clip;
  }
}

/* 极小屏幕特殊处理 */
@media (max-width: 375px) {
  .title-section h1 {
    font-size: 1.3rem;
  }
  
  .title-section h2 {
    font-size: 1.4rem;
  }
  
  .step-title {
    font-size: 1.1rem;
  }
  
  .content-icon {
    width: 150px;
    height: 150px;
  }
}

/* 触摸设备优化 */
@media (hover: none) and (pointer: coarse) {
  .step-item:hover {
    transform: none;
  }
  
  .step-item:active {
    transform: translateX(3px);
    background-color: rgba(241, 245, 249, 0.9);
  }
}

/* 平板设备优化 */
@media (min-width: 769px) and (max-width: 1024px) {
  .content-icon {
    width: 280px;
    height: 280px;
  }
  
  .step-title {
    font-size: 1.4rem;
  }
  
  .step-desc {
    font-size: 1rem;
  }
}
</style>