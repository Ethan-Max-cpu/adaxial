<template>
  <div class="relative bg-white flex items-center justify-center overflow-hidden" :style="containerStyle">
    <!-- 背景图片 -->
    <div 
      class="absolute inset-0 bg-cover bg-center"
      :style="backgroundImageStyle"
    >
    </div>
    
    <div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center w-full pt-12 sm:pt-0">
      <!-- 标题 -->
      <transition name="slide-up" appear>
        <h1 class="text-4xl font-extrabold tracking-tight text-gray-900 sm:text-5xl lg:text-6xl drop-shadow-lg">
          WELCOME TO 
          <span class="text-green-400">Adaxial</span>
        </h1>
      </transition>

      <!-- 描述 - 字体小一号 -->
      <transition name="fade-in" appear>
        <p class="mt-6 text-base sm:text-lg text-gray-900 max-w-3xl mx-auto px-4 drop-shadow-lg">
          Agency Ad Accounts. Unlimited accounts. No spend limits. Free replacements.
        </p>
      </transition>

      <!-- 按钮组 - 修改为两个按钮 -->
      <transition-group 
        name="staggered-fade" 
        tag="div"
        class="mt-10 flex flex-col sm:flex-row justify-center items-center gap-4 sm:gap-6"
        appear
      >
        <!-- Get started 按钮 -->
        <a 
          key="start"
          href="#pricing-section"
          class="inline-flex items-center justify-center px-8 py-4 border border-transparent text-base sm:text-lg font-medium rounded-lg text-white bg-green-600 hover:bg-green-700 transition-all duration-300 transform hover:scale-105 cursor-pointer w-full sm:w-auto shadow-lg hover:shadow-xl"
          @click.prevent="scrollToPricing"
        >
          Get Started
        </a>
        
        <!-- 新增 LET'S TALK 按钮 -->
        <a 
          key="talk"
          href="#faq-section" 
          class="inline-flex items-center justify-center px-8 py-4 border border-transparent text-base sm:text-lg font-medium rounded-lg text-white bg-green-600 hover:bg-green-700 transition-all duration-300 transform hover:scale-105 cursor-pointer w-full sm:w-auto shadow-lg hover:shadow-xl"
          @click.prevent="scrollToFAQ"
        >
          Let's Talk
        </a>
      </transition-group>
    </div>
  </div>
</template>

<script setup>
import { onMounted, computed } from 'vue'

// 导入背景图片
import backgroundImage from '@/assets/images/welcome-background.jpg'

// 背景图片样式
const backgroundImageStyle = computed(() => ({
  backgroundImage: `url(${backgroundImage})`,
  backgroundPosition: 'center',
  backgroundSize: 'cover',
  backgroundAttachment: 'fixed' // 添加视差滚动效果
}))

// 计算容器高度为屏幕的70%
const containerStyle = computed(() => ({
  height: '70vh',
  minHeight: '500px' // 确保移动端也有足够高度
}))

onMounted(() => {
  // 可以在这里添加其他初始化逻辑
})

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

// 平滑滚动到FAQ区域
const scrollToFAQ = () => {
  const pricingElement = document.getElementById('faq-section')
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
/* Vue 过渡动画 */
.slide-up-enter-active,
.slide-up-leave-active {
  transition: all 0.8s ease;
}

.slide-up-enter-from {
  opacity: 0;
  transform: translateY(30px);
}

.slide-up-enter-to {
  opacity: 1;
  transform: translateY(0);
}

.fade-in-enter-active,
.fade-in-leave-active {
  transition: all 0.8s ease 0.3s;
}

.fade-in-enter-from {
  opacity: 0;
}

.fade-in-enter-to {
  opacity: 1;
}

.staggered-fade-enter-active {
  transition: all 0.6s ease;
}

.staggered-fade-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

.staggered-fade-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

/* 为每个按钮设置不同的延迟 */
.staggered-fade-enter-active:nth-child(1) {
  transition-delay: 0.6s;
}

.staggered-fade-enter-active:nth-child(2) {
  transition-delay: 0.8s;
}

/* 移动端适配 */
@media (max-width: 640px) {
  .relative.max-w-7xl {
    padding-top: 2rem;
  }
  
  h1 {
    font-size: 2.5rem;
    line-height: 1.2;
  }
  
  /* 移动端描述字体也小一号 */
  p {
    font-size: 1rem; /* 从1.125rem改为1rem */
    padding-left: 1rem;
    padding-right: 1rem;
  }
  
  .mt-10 {
    margin-top: 2rem;
  }
  
  /* 移动端按钮优化 */
  a {
    width: 100%;
    max-width: 280px;
  }
  
  /* 移动端背景图片优化 */
  .bg-cover {
    background-attachment: scroll; /* 移动端移除视差效果 */
  }
  
  /* 移动端遮罩层优化 */
  .bg-gradient-to-r {
    background: linear-gradient(to bottom, rgba(0,0,0,0.7), rgba(0,0,0,0.5));
  }
}

/* 平板适配 */
@media (min-width: 641px) and (max-width: 768px) {
  h1 {
    font-size: 3rem;
  }
  
  /* 平板端描述字体也小一号 */
  p {
    font-size: 1.125rem; /* 从1.25rem改为1.125rem */
  }
  
  /* 平板端按钮稍微调整 */
  a {
    padding-left: 2rem;
    padding-right: 2rem;
  }
}

/* 小屏幕手机适配 */
@media (max-width: 480px) {
  h1 {
    font-size: 2rem;
  }
  
  /* 小屏幕描述字体也小一号 */
  p {
    font-size: 0.875rem; /* 从1rem改为0.875rem */
  }
  
  /* 容器最小高度在超小屏幕上适当减小 */
  .relative.bg-white {
    min-height: 400px;
  }
  
  .relative.max-w-7xl {
    padding-top: 1.5rem;
  }
  
  .mt-10 {
    margin-top: 1.5rem;
  }
  
  a {
    padding-left: 1.5rem;
    padding-right: 1.5rem;
    padding-top: 0.875rem;
    padding-bottom: 0.875rem;
  }
  
  /* 小屏幕背景优化 */
  .bg-center {
    background-position: 50% 30%; /* 在移动端调整背景位置 */
  }
}

/* 大屏幕优化 */
@media (min-width: 1400px) {
  h1 {
    font-size: 4rem;
  }
  
  /* 大屏幕描述字体也小一号 */
  p {
    font-size: 1.25rem; /* 从1.5rem改为1.25rem */
  }
  
  /* 大屏幕增强视差效果 */
  .bg-cover {
    background-attachment: fixed;
  }
}

/* 触摸设备优化 */
@media (hover: none) and (pointer: coarse) {
  a:hover {
    transform: none;
  }
  
  a:active {
    transform: scale(0.98);
  }
}

/* 打印时隐藏背景 */
@media print {
  .absolute.inset-0 {
    display: none;
  }
}
</style>