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
              <div class="content-icon">
                <i :class="currentStep.icon"></i>
              </div>
              <h3 class="content-title">{{ currentStep.contentTitle }}</h3>
              <p class="content-text">{{ currentStep.contentText }}</p>
              
              <!-- 用户ID信息 - 仅在第一个步骤显示 -->
              <div v-if="currentStepIndex === 0" class="user-info-section">
                <div class="user-id">用户318351</div>
                <div class="user-note">请根据您的业务需求提供详细信息</div>
              </div>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'StepsComponent',
  data() {
    return {
      currentStepIndex: 0,
      steps: [
        {
          title: 'Submit Your Business Info',
          description: 'Tell us about your website and business so we can assess if you\'re the right fit for our premium ad accounts.',
          icon: 'fas fa-user-tie',
          contentTitle: 'Submit Business Info',
          contentText: 'Tell us about your website and business so we can assess if you\'re the right fit for our premium ad accounts.'
        },
        {
          title: 'Fund Your Account Easily',
          description: 'Once approved, your agency account is delivered within 24 hours. Fund via card, crypto, or direct bank transfer.',
          icon: 'fas fa-credit-card',
          contentTitle: 'Fund Your Account',
          contentText: 'Once approved, your agency account is delivered within 24 hours. Fund via card, crypto, or direct bank transfer.'
        },
        {
          title: 'Launch Ads with Confidence',
          description: 'Start running ads immediately—with stable accounts designed for scale and full ban protection.',
          icon: 'fas fa-rocket',
          contentTitle: 'Launch Ads',
          contentText: 'Start running ads immediately—with stable accounts designed for scale and full ban protection.'
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

/* 主容器 - 无任何外边距，占满整个屏幕 */
.steps-component {
  background: linear-gradient(135deg, #0a0a0a, #1a1a1a);
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
  border-bottom: 1px solid #2a2a2a;
}

.title-container {
  width: 100%;
  max-width: 1400px; /* 增加最大宽度确保有足够空间 */
  padding: 0 100px; /* 增加左右内边距 */
  text-align: center;
}

.title-section h1 {
  font-size: 3rem; /* 稍微减小字体大小 */
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

.title-section h2 {
  font-size: 2.2rem; /* 稍微减小字体大小 */
  color: #ffffff;
  margin-bottom: 15px;
  font-weight: 700;
  line-height: 1.2;
}

/* 关键优化：确保副标题在一行内显示 */
.title-section .subtitle {
  font-size: 1.2rem; /* 减小字体大小 */
  color: #bbbbbb;
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

/* 左侧步骤列表 */
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
  background-color: rgba(26, 26, 26, 0.7);
  width: 100%;
}

.step-item:hover {
  background-color: rgba(38, 38, 38, 0.9);
  transform: translateX(3px);
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2);
}

.step-item.active {
  background-color: rgba(38, 38, 38, 0.9);
  border-left: 4px solid #7d5fff;
  box-shadow: 0 5px 15px rgba(125, 95, 255, 0.2);
}

.step-number {
  font-size: 0.9rem;
  color: #7d5fff;
  font-weight: 700;
  margin-bottom: 8px;
  letter-spacing: 1.2px;
  text-transform: uppercase;
}

.step-title {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 8px;
  color: #ffffff;
  line-height: 1.3;
}

.step-desc {
  font-size: 1.05rem;
  color: #cccccc;
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
  background: linear-gradient(135deg, #1a2a6c, #2a3a9c, #3a4acc);
  border-radius: 16px;
  padding: 30px 25px;
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  box-shadow: 0 15px 30px rgba(26, 42, 108, 0.5);
  position: relative;
  overflow: hidden;
  height: 100%;
  width: 100%;
}

.content-display::before {
  content: '';
  position: absolute;
  top: -30%;
  right: -30%;
  width: 250px;
  height: 250px;
  background: rgba(255, 255, 255, 0.05);
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
  background: rgba(255, 255, 255, 0.03);
  border-radius: 50%;
  z-index: 0;
}

.content-icon {
  width: 100px;
  height: 100px;
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 25px;
  font-size: 2.5rem;
  color: #ffffff;
  z-index: 1;
  border: 2px solid rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(8px);
}

.content-title {
  font-size: 1.9rem;
  font-weight: 700;
  margin-bottom: 20px;
  color: #ffffff;
  z-index: 1;
  line-height: 1.2;
}

.content-text {
  font-size: 1.1rem;
  line-height: 1.5;
  color: #e6e6e6;
  max-width: 400px;
  margin-bottom: 15px;
  z-index: 1;
  font-weight: 400;
}

.user-info-section {
  margin-top: 25px;
  padding-top: 20px;
  border-top: 1px solid rgba(255, 255, 255, 0.3);
  width: 100%;
  max-width: 350px;
  z-index: 1;
}

.user-id {
  font-size: 1.4rem;
  font-weight: 700;
  color: #ffffff;
  margin-bottom: 8px;
  letter-spacing: 1px;
}

.user-note {
  font-size: 1rem;
  color: #cccccc;
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
  
  .title-section h1 {
    font-size: 2.6rem;
  }
  
  .title-section h2 {
    font-size: 1.9rem;
  }
  
  /* 在较小屏幕上允许副标题换行 */
  .title-section .subtitle {
    white-space: normal;
    max-width: 900px;
  }
  
  .step-title {
    font-size: 1.4rem;
  }
  
  .content-title {
    font-size: 1.7rem;
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
    font-size: 2.2rem;
  }
  
  .title-section h2 {
    font-size: 1.6rem;
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
    font-size: 1.2rem;
  }
  
  .step-desc {
    font-size: 1rem;
  }
  
  .content-display {
    padding: 25px 20px;
  }
  
  .content-icon {
    width: 80px;
    height: 80px;
    font-size: 2rem;
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
    font-size: 1.8rem;
  }
  
  .title-section h2 {
    font-size: 1.3rem;
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
    font-size: 1.1rem;
  }
  
  .step-desc {
    font-size: 0.9rem;
  }
  
  .content-display {
    padding: 20px 15px;
  }
  
  .content-icon {
    width: 70px;
    height: 70px;
    font-size: 1.8rem;
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
  .title-section .subtitle {
    white-space: normal;
    line-height: 1.5;
    text-overflow: clip;
  }
}
</style>