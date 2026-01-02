<template>
  <div>
    <!-- Hero Section -->
    <!-- <div class="relative bg-black min-h-screen flex items-center justify-center">
      <div class="absolute inset-0 bg-gradient-to-r from-black to-gray-900"></div>
      <div class="relative max-w-7xl mx-auto py-24 px-4 sm:py-32 sm:px-6 lg:px-8 text-center w-full">
        <h1 class="text-4xl font-extrabold tracking-tight text-white sm:text-5xl lg:text-6xl">
          WELCOME TO <span class="text-green-500">ORANGE MEDIA</span>
        </h1>
        <p class="mt-6 text-xl text-white max-w-3xl mx-auto">
          Agency Ad Accounts. Unlimited accounts. No spend limits. Freereplacements.
        </p>
        <div class="mt-10 flex justify-center space-x-4">
          <router-link to="/services"
            class="inline-flex items-center px-8 py-4 border border-transparent text-lg font-medium rounded-sm text-white bg-green-600 hover:bg-green-700 transition-colors duration-200">
            Get started
          </router-link>
          <a href="https://t.me/luluyanyan2002" target="_blank"
            class="inline-flex items-center px-8 py-4 border border-transparent text-lg font-medium rounded-sm text-white bg-green-600 hover:bg-green-700 transition-colors duration-200">
            Join Telegram
          </a>
          <a href="https://api.whatsapp.com/send?phone=8618603352371&text=hello" target="_blank"
            class="inline-flex items-center px-8 py-4 border border-transparent text-lg font-medium rounded-sm text-white bg-green-600 hover:bg-green-700 transition-colors duration-200">
            Join Whatsapp
          </a>
        </div>
      </div>
    </div> -->

    <!-- 按顺序引入子组件 -->
    <WelcomeComponent />
    <AboutusComponent />
    <WhyadawakenComponent />
    <StepsComponent />
    <TestimonialsComponent />
    <PricingComponent id="pricing-section" />
    <FAQComponent id="faq-section"/>
  </div>
</template>

<script setup>
// 引入子组件
import StepsComponent from './Home/StepsComponent.vue'
import AboutusComponent from './Home/AboutusComponent.vue'
import WhyadawakenComponent from './Home/WhyadawakenComponent.vue'
import TestimonialsComponent from './Home/TestimonialsComponent.vue'
import PricingComponent from './Home/PricingComponent.vue'
import FAQComponent from './Home/FAQComponent.vue'
import WelcomeComponent from './Home/WelcomeComponent.vue'
</script>

<style scoped>
</style>