<template>
  <div class="bg-white min-h-screen py-8 md:py-16 px-4 md:px-6">
    <!-- 顶部平台图标 - 可切换 -->
    <div class="max-w-7xl mx-auto">
      <!-- 移动端平台选择器 -->
      <div class="md:hidden mb-8 relative">
        <select 
          v-model="activePlatform" 
          class="w-full bg-gray-50 text-gray-800 border border-gray-300 py-3 px-4 text-base appearance-none rounded-lg"
        >
          <option 
            v-for="platform in platforms" 
            :key="platform.id" 
            :value="platform.id"
            class="bg-white"
          >
            {{ platform.name }}
          </option>
        </select>
        <!-- 自定义下拉箭头 -->
        <div class="absolute right-4 top-1/2 transform -translate-y-1/2 pointer-events-none">
          <svg class="w-5 h-5 text-gray-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
          </svg>
        </div>
      </div>

      <!-- 桌面端平台选择器 -->
      <div class="hidden md:flex justify-center space-x-8 lg:space-x-12 mb-8 md:mb-16">
        <div 
          v-for="platform in platforms" 
          :key="platform.id"
          @click="selectPlatform(platform.id)"
          class="relative cursor-pointer group"
        >
          <div 
            class="text-xl md:text-2xl lg:text-3xl font-bold transition-all duration-300 transform group-hover:scale-105"
            :class="[
              activePlatform === platform.id 
                ? 'text-gray-900 drop-shadow-sm' 
                : 'text-gray-400 hover:text-gray-600'
            ]"
          >
            {{ platform.name }}
          </div>
          <!-- 激活指示器 -->
          <div 
            v-if="activePlatform === platform.id"
            class="absolute -bottom-2 md:-bottom-3 left-1/2 transform -translate-x-1/2 w-12 md:w-16 h-0.5 md:h-1 rounded-full"
            :class="platform.activeGradient"
          ></div>
        </div>
      </div>

      <!-- 根据平台筛选的套餐卡片 -->
      <div class="flex flex-wrap justify-center gap-4 md:gap-6 lg:gap-8">
        <!-- 遍历当前平台的所有套餐 -->
        <div 
          v-for="(plan, index) in filteredPlans" 
          :key="plan.id"
          class="relative w-full sm:w-[calc(100%-2rem)] md:w-[calc(50%-1rem)] lg:w-[calc(25%-1.5rem)] max-w-sm"
        >
          <!-- Most Popular 徽章 - 优化移动端显示 -->
          <div v-if="plan.popular" class="absolute -top-3 md:-top-3 left-1/2 transform -translate-x-1/2 z-20">
            <div class="relative">
              <!-- 绿色背景 - 圆角设计 -->
              <span
                class="bg-gradient-to-r from-green-500 to-emerald-600 text-white text-xs md:text-xs font-black tracking-wider uppercase px-3 md:px-5 py-1.5 md:py-2 shadow-lg rounded-full"
              >
                MOST POPULAR
              </span>
              <!-- 下箭头装饰 -->
              <div class="absolute -bottom-1 left-1/2 transform -translate-x-1/2 w-0 h-0 
                border-l-[4px] md:border-l-[6px] border-l-transparent
                border-r-[4px] md:border-r-[6px] border-r-transparent
                border-t-[4px] md:border-t-[6px] border-t-emerald-600">
              </div>
            </div>
          </div>

          <!-- 卡片容器 - 移动端高度自适应 -->
          <div
            class="relative h-auto md:h-[650px] min-h-[580px] md:min-h-[650px] overflow-hidden transition-transform duration-300 hover:scale-[1.02] border border-gray-200 rounded-xl shadow-md hover:shadow-lg"
            :class="plan.cardClasses">
            <!-- 卡片背景渐变层 -->
            <div class="absolute inset-0 rounded-xl" :class="plan.gradientBg"></div>

            <!-- 卡片内容 -->
            <div class="relative p-4 md:p-6 h-full flex flex-col">
              <!-- 套餐名称 -->
              <div style="text-align: center; margin-bottom: 1rem;">
                <h3 class="plan-title">
                  {{ plan.name }}
                </h3>
              </div>
              
              <!-- Get started 按钮 - 优化移动端 -->
              <div class="mb-4 md:mb-6">
                <button 
                  @click="handleSelectPlan(plan)"
                  class="w-full py-3 md:py-3 text-white font-semibold text-sm md:text-sm tracking-wider uppercase transition-all duration-300 relative overflow-hidden active:scale-95 rounded-lg"
                  :class="plan.buttonClasses"
                >
                  <span class="relative z-10">Get started</span>
                  <div
                    class="absolute inset-0 bg-gradient-to-r from-transparent via-white/20 to-transparent -translate-x-full animate-shimmer">
                  </div>
                </button>
              </div>

              <!-- 权益列表 - 优化移动端间距 -->
              <div class="space-y-2 md:space-y-3 flex-grow">
                <div 
                  v-for="(feature, featureIndex) in plan.features" 
                  :key="featureIndex" 
                  class="flex items-start"
                >
                  <!-- 小对号图标 -->
                  <div class="mr-2 md:mr-3 mt-0.5 flex-shrink-0">
                    <svg class="w-3.5 h-3.5 md:w-4 md:h-4 text-emerald-500" fill="currentColor" viewBox="0 0 20 20">
                      <path fill-rule="evenodd"
                        d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                        clip-rule="evenodd" />
                    </svg>
                  </div>
                  <!-- 使用解析函数 -->
                  <span 
                    class="text-xs md:text-sm text-gray-700 leading-relaxed" 
                    v-html="parseBoldText(feature)"
                  ></span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 当前选中的平台
const activePlatform = ref('meta') // 默认选中Meta

// 平台数据
const platforms = ref([
  { 
    id: 'meta', 
    name: 'Meta', 
    activeGradient: 'bg-gradient-to-r from-blue-500 to-emerald-500' 
  },
  { 
    id: 'other', 
    name: 'Other', 
    activeGradient: 'bg-gradient-to-r from-purple-500 to-indigo-500' 
  }
])

// 所有平台的套餐数据 - 更新样式以适配白色背景
const allPlans = ref({
  meta: [
    {
      id: 'meta-bronze',
      name: 'Meta',
      popular: false,
      cardClasses: 'bg-white/90 border border-gray-200 shadow-lg',
      gradientBg: 'bg-gradient-to-br from-amber-50/50 to-amber-100/30',
      buttonClasses: 'bg-gradient-to-r from-gray-800 to-gray-700 hover:from-gray-700 hover:to-gray-600 shadow-md',
      features: [
        '**Accepting All**',
        'Fee: 2.5%-4% (Depending on the spend ped day) Unlimited account supply',
        'Unlimited account supply',
        'Run Ads for Almost Any Vertical',
        'Strong agency ad account included',
        'Lifetime replacements on the ad account',
        '1x FB setup included ($300 value)',
        'Earn cashback or CC points',
        'No Bans & Restrictions **Reallocate balance between accounts if suspended**'
      ]
    },
    {
      id: 'meta-gold',
      name: 'TikTok',
      popular: false,
      cardClasses: 'bg-white/90 border border-gray-200 shadow-lg',
      gradientBg: 'bg-gradient-to-br from-amber-50/50 to-amber-100/30',
      buttonClasses: 'bg-gradient-to-r from-gray-800 to-gray-700 hover:from-gray-700 hover:to-gray-600 shadow-md',
      features: [
        '**Accepting All**',
        'Fee: 0%-6% (Depending on the spend ped day)',
        'Unlimited spend',
        'Unlimited account supply',
        'Target 55+ countries',
        'Reallocate balance between accounts if suspended',
        'Full access to advertising features (branding, conversion,...)',
        'Top up via Bank/Crypto（+1% fee） '
      ]
    },
    {
      id: 'meta-diamond',
      name: 'Google',
      popular: false,
      cardClasses: 'bg-white/90 border border-gray-200 shadow-lg',
      gradientBg: 'bg-gradient-to-br from-amber-50/50 to-amber-100/30',
      buttonClasses: 'bg-gradient-to-r from-gray-800 to-gray-700 hover:from-gray-700 hover:to-gray-600 shadow-md',
      features: [
        '**Only Whitehat**',
        'Fee: 1.5%-3% (Depending on the spend ped day)',
        'Unlimited spend',
        'Reallocate balance between accounts if suspended',
        'Top up via Bank/Crypto（+1% fee）'
      ]
    }
  ],
  other: [
    {
      id: 'other-bigo',
      name: 'Bigo',
      price: '$599',
      popular: false,
      cardClasses: 'bg-white/90 border border-gray-200 shadow-lg',
      gradientBg: 'bg-gradient-to-br from-amber-50/50 to-amber-100/30',
      buttonClasses: 'bg-gradient-to-r from-gray-800 to-gray-700 hover:from-gray-700 hover:to-gray-600 shadow-md',
      features: [
        '**Accepting All**',
        'No Fee',
        'No restrictions, No Prohibitions',
        'Unlimited spend',
        'Unlimited account supply',
        'Target 55+ countries',
        'Top Up via Bank/Crypto (+1%)'
      ]
    },
    {
      id: 'other-taboola',
      name: 'Taboola',
      price: '$599',
      popular: false,
      cardClasses: 'bg-white/90 border border-gray-200 shadow-lg',
      gradientBg: 'bg-gradient-to-br from-yellow-50/50 to-yellow-100/30',
      buttonClasses: 'bg-gradient-to-r from-gray-800 to-gray-700 hover:from-gray-700 hover:to-gray-600 shadow-md',
      features: [
        '**Accepting All**',
        'Fee：3%-9%',
        'No restrictions, No Prohibitions',
        'Unlimited spend',
        'Target 55+ countries   ',
        'Top Up via Bank/Crypto (+1%)'
      ]
    },
    {
      id: 'other-newsbreak',
      name: 'Newsbreak',
      price: '$399',
      popular: false,
      cardClasses: 'bg-white/90 border border-gray-200 shadow-lg',
      gradientBg: 'bg-gradient-to-br from-yellow-50/50 to-yellow-100/30',
      buttonClasses: 'bg-gradient-to-r from-gray-800 to-gray-700 hover:from-gray-700 hover:to-gray-600 shadow-md',
      features: [
        '**Only Whitehat**',
        'No Fee',
        'No restrictions, No Prohibitions',
        'Unlimited spend',
        'Unlimited account supply',
        'Target 55+ countries',
        'Top Up via Bank/Crypto (+1%)'
      ]
    },
    {
      id: 'other-snapchat',
      name: 'Snapchat',
      price: '$399',
      popular: false,
      cardClasses: 'bg-white/90 border border-gray-200 shadow-lg',
      gradientBg: 'bg-gradient-to-br from-amber-50/50 to-amber-100/30',
      buttonClasses: 'bg-gradient-to-r from-gray-800 to-gray-700 hover:from-gray-700 hover:to-gray-600 shadow-md',
      features: [
        '**Only Whitehat**',
        'No Fee',
        'No restrictions, No Prohibitions',
        'Unlimited spend',
        'Unlimited account supply',
        'Target 55+ countries',
        'Top Up via Bank/Crypto (+1%)'
      ]
    }
  ]
})

// 选择平台
const selectPlatform = (platformId) => {
  activePlatform.value = platformId
}

// 计算当前平台的套餐
const filteredPlans = computed(() => {
  return allPlans.value[activePlatform.value] || []
})

// 计算当前平台名称
const currentPlatformName = computed(() => {
  const platform = platforms.value.find(p => p.id === activePlatform.value)
  return platform ? platform.name : ''
})

// 选择套餐 - 修改为跳转WhatsApp链接
const handleSelectPlan = (plan) => {
  const whatsappUrl = `https://api.whatsapp.com/send?phone=8618603352371&text=hello`;
  window.open(whatsappUrl, '_blank');
}

// 解析加粗标记的函数
const parseBoldText = (text) => {
  if (!text) return ''
  return text.replace(/\*\*(.*?)\*\*/g, '<strong class="font-bold text-gray-900">$1</strong>')
}
</script>

<style>
/* 自定义动画 */
@keyframes shimmer {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(100%);
  }
}

.animate-shimmer {
  animation: shimmer 2s infinite;
}

/* 套餐名称样式 - 增加字体大小并居中 */
.plan-title {
  font-weight: 700; /* 加粗 */
  text-align: center; /* 居中 */
  color: #111827; /* 深灰色 */
  margin: 0 0 0.5rem 0; /* 底部间距 */
  padding: 0;
  line-height: 1.2;
  
  /* 桌面端 - 大字体 */
  font-size: 2.5rem; /* 40px - 显著增加 */
  letter-spacing: -0.025em; /* 稍微收紧字间距 */
}

/* 移动端字体大小 */
@media (max-width: 767px) {
  .plan-title {
    font-size: 1.875rem; /* 30px - 移动端也大幅增加 */
  }
}

/* 平板设备优化 */
@media (min-width: 768px) and (max-width: 1023px) {
  .plan-title {
    font-size: 2.25rem; /* 36px - 平板端 */
  }
}

/* 桌面大屏幕 */
@media (min-width: 1024px) {
  .plan-title {
    font-size: 2.5rem; /* 40px */
  }
}

/* 超宽屏幕额外增大 */
@media (min-width: 1280px) {
  .plan-title {
    font-size: 2.75rem; /* 44px - 在超宽屏幕上更大 */
  }
}

/* 移动端优化 */
@media (max-width: 767px) {
  /* 卡片容器移动端优化 */
  .min-h-\[580px\] {
    min-height: 520px; /* 移动端稍微减少高度 */
  }
  
  /* 按钮优化 */
  button[class*="Get started"]:active {
    transform: scale(0.98);
  }
  
  /* 卡片间距优化 */
  .gap-4 > * {
    margin-bottom: 1rem; /* 16px */
  }
  
  /* 平台选择器在移动端优化 */
  .md\\:hidden select {
    font-size: 1rem; /* 16px */
  }
}

/* 平板设备优化 */
@media (min-width: 768px) and (max-width: 1023px) {
  /* 卡片宽度调整为每行2个 - 需要根据实际类名调整 */
  .md-w-calc-50-1rem {
    width: calc(50% - 1rem);
  }
  
  /* 卡片高度调整 - 需要根据实际类名调整 */
  .md-h-650px {
    height: 600px;
  }
  
  .md-min-h-650px {
    min-height: 600px;
  }
}

/* 移动端下拉菜单样式优化 */
select {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' fill='none' viewBox='0 0 20 20'%3e%3cpath stroke='%236b7280' stroke-linecap='round' stroke-linejoin='round' stroke-width='1.5' d='M6 8l4 4 4-4'/%3e%3c/svg%3e");
  background-position: right 0.5rem center;
  background-repeat: no-repeat;
  background-size: 1.5em 1.5em;
  padding-right: 2.5rem;
  border-radius: 0.5rem; /* 8px */
  transition: all 0.2s ease;
}

select:focus {
  outline: none;
  border-color: #3b82f6; /* blue-500 */
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}
</style>