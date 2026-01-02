<template>
  <nav class="bg-white shadow-md fixed w-full z-50 border-b-2 border-green-600">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 ">
      <div class="flex justify-between h-16">
        <!-- Logo -->
        <div class="flex-shrink-0 flex items-center">
          <router-link to="/" class="flex items-center">
            <!-- 替换这里的文字为图片 -->
            <!-- <img :src="logo" alt="Orange Media Logo" class="h-12 w-auto"> -->
            <span class="text-2xl font-bold text-gray-900">Adaxial</span>
          </router-link>
        </div>

        <!-- 桌面端导航 -->
        <div class="hidden md:flex items-center space-x-2"> <!-- 减小间距 -->
          <router-link 
            v-for="item in navItems" 
            :key="item.path"
            :to="item.path"
            class="text-gray-600 hover:text-gray-900 px-4 py-3 text-sm font-medium transition-colors duration-200 rounded-md"
            :class="{ 
              'text-white bg-green-600': $route.path === item.path,
              'hover:bg-gray-100': $route.path !== item.path
            }"
          >
            {{ item.name }}
          </router-link>
        </div>

        <!-- 移动端菜单按钮 -->
        <div class="md:hidden flex items-center">
          <button @click="isOpen = !isOpen" class="inline-flex items-center justify-center p-2 rounded-md text-gray-600 hover:text-gray-900 hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-green-500">
            <span class="sr-only">打开主菜单</span>
            <svg class="h-6 w-6" :class="{ 'hidden': isOpen, 'block': !isOpen }" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
            <svg class="h-6 w-6" :class="{ 'hidden': !isOpen, 'block': isOpen }" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- 移动端菜单 - 背景也改为浅色 -->
    <div class="md:hidden bg-white shadow-lg border-t border-gray-200" :class="{ 'block': isOpen, 'hidden': !isOpen }">
      <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
        <router-link 
          v-for="item in navItems" 
          :key="item.path"
          :to="item.path"
          class="block px-4 py-3 text-base font-medium text-gray-600 hover:text-gray-900 rounded-md"
          :class="{ 
            'text-white bg-green-600': $route.path === item.path,  
            'hover:bg-gray-100': $route.path !== item.path
          }"
          @click="isOpen = false"
        >
          {{ item.name }}
        </router-link>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const isOpen = ref(false)

const navItems = [
  { name: 'PORTFOLIO', path: '/' },
  { name: '联系我们', path: '/contact' }
]
</script>

<style scoped>
/* 添加过渡动画 */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* 移动端适配 */
@media (max-width: 768px) {
  nav {
    padding-left: 0.5rem;
    padding-right: 0.5rem;
  }
  
  .h-16 {
    height: 3.5rem; /* 稍微减小移动端高度 */
  }
  
  .text-2xl {
    font-size: 1.5rem; /* 移动端Logo字体稍小 */
  }
  
  /* 移动端菜单按钮样式优化 */
  button {
    padding: 0.5rem;
  }
  
  .h-6.w-6 {
    height: 1.5rem;
    width: 1.5rem;
  }
  
  /* 移动端菜单项内边距调整 */
  .px-4.py-3 {
    padding-left: 1rem;
    padding-right: 1rem;
    padding-top: 0.75rem;
    padding-bottom: 0.75rem;
  }
  
  .text-base {
    font-size: 1rem;
  }
}

/* 小屏幕手机适配 */
@media (max-width: 480px) {
  .h-16 {
    height: 3rem; /* 进一步减小移动端高度 */
  }
  
  .text-2xl {
    font-size: 1.25rem; /* 进一步减小Logo字体 */
  }
  
  .space-y-1 {
    padding-top: 0.5rem;
    padding-bottom: 0.5rem;
  }
  
  /* 移动端菜单内边距调整 */
  .px-4.py-3 {
    padding-left: 0.875rem;
    padding-right: 0.875rem;
    padding-top: 0.625rem;
    padding-bottom: 0.625rem;
  }
  
  .text-base {
    font-size: 0.9375rem;
  }
}

/* 平板设备适配 */
@media (min-width: 769px) and (max-width: 1024px) {
  .max-w-7xl {
    padding-left: 1.5rem;
    padding-right: 1.5rem;
  }
  
  .text-sm {
    font-size: 0.875rem;
  }
  
  .px-4.py-3 {
    padding-left: 0.75rem;
    padding-right: 0.75rem;
  }
}

/* 大屏幕适配 */
@media (min-width: 1025px) {
  .space-x-2 > * + * {
    margin-left: 0.5rem; /* 桌面端导航项间距 */
  }
}

/* 触摸设备优化 */
@media (hover: none) and (pointer: coarse) {
  a:hover {
    background-color: transparent;
  }
  
  a:active {
    background-color: #f3f4f6; /* gray-100 */
  }
  
  .bg-green-600:active {
    background-color: #059669; /* green-700 */
  }
  
  button:active {
    background-color: #f3f4f6;
  }
}
</style>