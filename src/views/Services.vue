<template>
  <div class="bg-black min-h-screen py-16 px-4">
    <!-- 顶部平台图标 - 可切换 -->
    <div class="max-w-7xl mx-auto">
      <div class="flex justify-center space-x-12 mb-16">
        <div 
          v-for="platform in platforms" 
          :key="platform.id"
          @click="selectPlatform(platform.id)"
          class="relative cursor-pointer group"
        >
          <div 
            class="text-4xl font-bold transition-all duration-300 transform group-hover:scale-110"
            :class="[
              activePlatform === platform.id 
                ? 'text-white drop-shadow-lg' 
                : 'text-gray-500 hover:text-gray-300'
            ]"
          >
            {{ platform.name }}
          </div>
          <!-- 激活指示器 -->
          <div 
            v-if="activePlatform === platform.id"
            class="absolute -bottom-3 left-1/2 transform -translate-x-1/2 w-16 h-1 rounded-full"
            :class="platform.activeGradient"
          ></div>
        </div>
      </div>

      <!-- 根据平台筛选的套餐卡片 -->
      <div class="flex flex-wrap justify-center gap-8">
        <!-- 遍历当前平台的所有套餐 -->
        <div 
          v-for="(plan, index) in filteredPlans" 
          :key="plan.id"
          class="relative w-full sm:w-[calc(50%-1rem)] lg:w-[calc(25%-1.5rem)] max-w-sm"
        >
      <!-- Most Popular 徽章 - 绿色尖锐设计 -->
      <div v-if="plan.popular" class="absolute -top-3 left-1/2 transform -translate-x-1/2 z-20">
        <div class="relative">
          <!-- 绿色背景 - 尖锐设计 -->
          <span
            class="bg-gradient-to-r from-green-500 to-emerald-600 text-white text-xs font-black tracking-wider uppercase px-5 py-2 shadow-lg"
            style="border-radius: 0;">
            MOST POPULAR
          </span>
          <!-- 下箭头装饰 -->
          <div class="absolute -bottom-1 left-1/2 transform -translate-x-1/2 w-0 h-0 
            border-l-[6px] border-l-transparent
            border-r-[6px] border-r-transparent
            border-t-[6px] border-t-emerald-600">
          </div>
        </div>
      </div>

          <!-- 卡片容器 - 移除圆角，改为尖锐边框 -->
          <div
            class="relative h-[700px] overflow-hidden transition-transform duration-300 hover:scale-[1.02] border border-gray-800"
            style="border-radius: 0;" :class="plan.cardClasses">
            <!-- 卡片背景渐变层 -->
            <div class="absolute inset-0" :class="plan.gradientBg" style="border-radius: 0;"></div>

            <!-- 卡片内容 -->
            <div class="relative p-6 h-full flex flex-col">
              <!-- 套餐名称和价格 -->
              <div class="mb-6">
                <h3 class="text-2xl font-bold text-white mb-2">{{ plan.name }}</h3>
                <div class="flex items-baseline">
                  <span class="text-4xl font-bold text-white">{{ plan.price }}</span>
                  <span class="text-gray-400 text-sm ml-2">/month</span>
                </div>
              </div>

              <!-- Get started 按钮 - 也改为尖锐边框 -->
              <div class="mb-6">
                <button @click="handleSelectPlan(plan)"
                  class="w-full py-3 text-white font-semibold text-sm tracking-wider uppercase transition-all duration-300 relative overflow-hidden"
                  style="border-radius: 0;" :class="plan.buttonClasses">
                  <!-- 白色边框效果 - 移除圆角 -->
                  <div class="absolute inset-0 border border-white/20 pointer-events-none" style="border-radius: 0;">
                  </div>
                  <span class="relative z-10">Get started</span>
                  <div
                    class="absolute inset-0 bg-gradient-to-r from-transparent via-white/10 to-transparent -translate-x-full animate-shimmer">
                  </div>
                </button>
              </div>

              <!-- 权益列表 - 缩短高度 -->
              <div class="space-y-3 flex-grow">
                <div v-for="(feature, featureIndex) in plan.features" :key="featureIndex" class="flex items-start">
                  <!-- 小对号图标 -->
                  <div class="mr-3 mt-0.5 flex-shrink-0">
                    <svg class="w-4 h-4 text-green-400" fill="currentColor" viewBox="0 0 20 20">
                      <path fill-rule="evenodd"
                        d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                        clip-rule="evenodd" />
                    </svg>
                  </div>
                  <!-- 使用解析函数 -->
                  <span class="text-sm text-gray-300 leading-relaxed" v-html="parseBoldText(feature)"></span>
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

// 平台数据 - 更新激活状态的渐变颜色
const platforms = ref([
  { 
    id: 'meta', 
    name: 'Meta', 
    activeGradient: 'bg-gradient-to-r from-blue-500 to-green-500' 
  },
  { 
    id: 'tiktok', 
    name: 'TikTok', 
    activeGradient: 'bg-gradient-to-r from-blue-500 to-green-500' 
  },
  { 
    id: 'google', 
    name: 'Google', 
    activeGradient: 'bg-gradient-to-r from-blue-500 to-green-500' 
  },
  { 
    id: 'other', 
    name: 'Other', 
    activeGradient: 'bg-gradient-to-r from-blue-500 to-green-500' 
  }
])

// 所有平台的套餐数据 - 精简样式配置
const allPlans = ref({
  // Meta平台套餐
  meta: [
    {
      id: 'meta-bronze',
      name: 'Bronze',
      price: '$299',
      popular: false,
      // 卡片样式
      cardClasses: 'bg-gradient-to-br from-gray-900/90 to-gray-950/90 border border-gray-800/50 shadow-lg',
      gradientBg: 'bg-gradient-to-br from-amber-900/10 to-amber-700/5',
      // 按钮样式
      buttonClasses: 'bg-gradient-to-r from-gray-900 to-gray-800 hover:from-gray-800 hover:to-gray-700 shadow-inner',
      // 权益
      features: [
        '**Only Whitehat**',
        'Fee: 0%-1% (Depending on the spend ped day)',
        'Up to $3k/month in spend',
        'Strong agency ad account included',
        'Top up via Bank/Crypto'
      ]
    },
    {
      id: 'meta-gold',
      name: 'Gold',
      price: '$599',
      popular: false,
      cardClasses: 'bg-gradient-to-br from-gray-900/90 to-gray-950/90 border border-gray-800/50 shadow-lg',
      gradientBg: 'bg-gradient-to-br from-yellow-900/10 to-yellow-700/5',
      buttonClasses: 'bg-gradient-to-r from-gray-900 to-gray-800 hover:from-gray-800 hover:to-gray-700 shadow-inner',
      features: [
        '**Only Whitehat**',
        'Fee: 0%-1% (Depending on the spend ped day)',
        'Up to $6k/month in spend',
        'Strong agency ad account included',
        '1x FB setup included ($300 value)',
        'Top up via Bank/Crypto'
      ]
    },
    {
      id: 'meta-diamond',
      name: 'Diamond',
      price: '$799',
      popular: true,
      cardClasses: 'bg-gradient-to-br from-green-900/20 to-green-950/20 border border-green-700/30 shadow-xl',
      gradientBg: 'bg-gradient-to-br from-green-700/15 to-emerald-700/10',
      buttonClasses: 'bg-gradient-to-r from-gray-900 to-gray-800 hover:from-gray-800 hover:to-gray-700 shadow-inner',
      features: [
        '**Accepting Whitehat/Grayhat**',
        'Fee: 4.5%-6% (Depending on the spend ped day) Unlimited account supply',
        'Unlimited account supply',
        'Run Ads for Almost Any Vertical',
        'Strong agency ad account included',
        'Lifetime replacements on the ad account',
        '1x FB setup included ($300 value)',
        'Top up via Bank/Crypto'
      ]
    },
    {
      id: 'meta-platinum',
      name: 'Platinum',
      price: '$1,499',
      popular: false,
      cardClasses: 'bg-gradient-to-br from-gray-900/90 to-gray-950/90 border border-gray-800/50 shadow-lg',
      gradientBg: 'bg-gradient-to-br from-blue-900/10 to-cyan-700/5',
      buttonClasses: 'bg-gradient-to-r from-gray-900 to-gray-800 hover:from-gray-800 hover:to-gray-700 shadow-inner',
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
    }
  ],
  // TikTok平台套餐
  tiktok: [
    {
      id: 'tiktok-bronze',
      name: 'Bronze',
      price: '$299',
      popular: false,
      cardClasses: 'bg-gradient-to-br from-gray-900/90 to-gray-950/90 border border-gray-800/50 shadow-lg',
      gradientBg: 'bg-gradient-to-br from-red-900/10 to-pink-700/5',
      buttonClasses: 'bg-gradient-to-r from-gray-900 to-gray-800 hover:from-gray-800 hover:to-gray-700 shadow-inner',
      features: [
        '**Only Whitehat**',
        'Fee: 2%-3% (Depending on the spend ped day)',
        'Unlimited spend',
        'Reallocate balance between accounts if suspended',
        'Top Up via Bank/Crypto '
      ]
    },
    {
      id: 'tiktok-gold',
      name: 'Gold',
      price: '$599',
      popular: false,
      cardClasses: 'bg-gradient-to-br from-gray-900/90 to-gray-950/90 border border-gray-800/50 shadow-lg',
      gradientBg: 'bg-gradient-to-br from-red-900/10 to-pink-700/5',
      buttonClasses: 'bg-gradient-to-r from-gray-900 to-gray-800 hover:from-gray-800 hover:to-gray-700 shadow-inner',
      features: [
        '**Only Whitehat**',
        'Fee: 0%-2% (Depending on the spend ped day)',
        'Unlimited spend',
        'Reallocate balance between accounts if suspended',
        'Top Up via Bank/Crypto '
      ]
    },
    {
      id: 'tiktok-diamond',
      name: 'Diamond',
      price: '$799',
      popular: true,
      cardClasses: 'bg-gradient-to-br from-green-900/20 to-green-950/20 border border-green-700/30 shadow-xl',
      gradientBg: 'bg-gradient-to-br from-green-700/15 to-emerald-700/10',
      buttonClasses: 'bg-gradient-to-r from-gray-900 to-gray-800 hover:from-gray-800 hover:to-gray-700 shadow-inner',
      features: [
        '**Accepting Whitehat/Grayhat.**',
        'Fee: 0%-6% (Depending on the spend ped day)',
        'Unlimited spend',
        'Unlimited account supply',
        'Target 55+ countries',
        'Reallocate balance between accounts if suspended',
        'Top Up via Bank/Crypto '
      ]
    },
    {
      id: 'tiktok-platinum',
      name: 'Platinum',
      price: '$1499',
      popular: false,
      cardClasses: 'bg-gradient-to-br from-gray-900/90 to-gray-950/90 border border-gray-800/50 shadow-lg',
      gradientBg: 'bg-gradient-to-br from-red-900/10 to-pink-700/5',
      buttonClasses: 'bg-gradient-to-r from-gray-900 to-gray-800 hover:from-gray-800 hover:to-gray-700 shadow-inner',
      features: [
        '**Accepting All**',
        'Fee: 0%-6% (Depending on the spend ped day)',
        'Unlimited spend',
        'Unlimited account supply',
        'Target 55+ countries',
        'Reallocate balance between accounts if suspended',
        'Full access to advertising features (branding, conversion,...)',
        'Top Up via Bank/Crypto '
      ]
    }
  ],
  // Google平台套餐
  google: [
    {
      id: 'google-starter',
      name: 'Starter',
      price: '$349',
      popular: true,
      cardClasses: 'bg-gradient-to-br from-green-900/20 to-green-950/20 border border-green-700/30 shadow-xl',
      gradientBg: 'bg-gradient-to-br from-green-700/15 to-emerald-700/10',
      buttonClasses: 'bg-gradient-to-r from-gray-900 to-gray-800 hover:from-gray-800 hover:to-gray-700 shadow-inner',
      features: [
        '**Only Whitehat**',
        'Fee: 1.5%-3% (Depending on the spend ped day)',
        'Unlimited spend',
        'Reallocate balance between accounts if suspended',
        'Top Up via Bank/Crypto'
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

// 选择套餐
const handleSelectPlan = (plan) => {
  console.log('Selected plan:', plan)
  // 这里可以添加选择套餐的逻辑，比如跳转到购买页面
  alert(`选择了 ${plan.name} 套餐 (${currentPlatformName.value}平台)`)
}

// 解析加粗标记的函数
const parseBoldText = (text) => {
  if (!text) return ''
  return text.replace(/\*\*(.*?)\*\*/g, '<strong class="font-bold text-white">$1</strong>')
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

/* 优化按钮锐化效果 */
button[class*="Get started"] {
  filter: drop-shadow(0 0 1px rgba(255, 255, 255, 0.3)) 
          drop-shadow(0 1px 2px rgba(0, 0, 0, 0.5));
}

/* 优化卡片阴影 */
[class*="shadow-lg"] {
  box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.3), 0 8px 10px -6px rgba(0, 0, 0, 0.2);
}

[class*="shadow-xl"] {
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.3), 0 10px 10px -6px rgba(0, 0, 0, 0.2);
}

/* 优化文字锐利度 */
.text-white {
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.3);
}

/* 按钮边框锐化 */
button[class*="Get started"] > div {
  border-width: 1px;
}
</style>