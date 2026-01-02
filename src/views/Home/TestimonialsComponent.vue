<!-- UserCommentsCarousel.vue -->
<template>
  <div class="comments-carousel-container">
    <!-- 滑动区域容器 -->
    <div 
      class="carousel-track-container"
      @mouseenter="pauseAutoScroll"
      @mouseleave="resumeAutoScroll"
    >
      <!-- 滑动轨道 - 实现无缝循环 -->
      <div 
        class="comments-track" 
        :style="{ transform: `translateX(${translateX}px)` }"
        ref="trackRef"
      >
        <!-- 使用精确的图片数据 -->
        <div 
          v-for="(comment, index) in allComments" 
          :key="`comment-${index}`" 
          class="comment-card"
        >
          <!-- 星级评分 -->
          <div class="rating">
            <el-icon v-for="i in 5" :key="i" class="star-icon">
              <StarFilled />
            </el-icon>
          </div>
          
          <!-- 评论标题 -->
          <h3 class="comment-title">{{ comment.title }}</h3>
          
          <!-- 评论内容 -->
          <p class="comment-content">{{ comment.content }}</p>
          
          <!-- 用户信息 -->
          <div class="user-info">
            <div class="user-avatar">
              <!-- 修改这里：从文字改为图片 -->
              <img 
                :src="comment.avatar" 
                :alt="comment.user"
                class="avatar-img"
              >
            </div>
            <div class="user-details">
              <p class="user-name">{{ comment.user }}</p>
              <p class="user-role">{{ comment.role }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { StarFilled } from '@element-plus/icons-vue'

// 导入头像图片
import avatar1 from '@/assets/avatars/avatar-01.jpg';
import avatar2 from '@/assets/avatars/avatar-02.jpg';
import avatar3 from '@/assets/avatars/avatar-03.jpg';
import avatar4 from '@/assets/avatars/avatar-04.jpg';
import avatar5 from '@/assets/avatars/avatar-05.jpg';
import avatar6 from '@/assets/avatars/avatar-06.jpg';
import avatar7 from '@/assets/avatars/avatar-07.jpg';

// 使用图片中的精确数据，添加 avatar 属性
const comments = ref([
  {
    title: "Exceptional User Experience & Conversion-Driving Precision",
    content: "Your media ad accounts are absolutely fantastic! The interface is super user-friendly, and the targeting options are so precise that our ad campaigns have seen a huge jump in conversion rates. Plus, your customer support is always quick to respond—you guys are total lifesavers!",
    user: "Bella",
    role: "",
    avatar: avatar1  // 添加头像属性
  },
  {
    title: "Reliable Performance & Top-Tier Analytics Tools",
    content: "We've tried several ad account providers before, but none compare to yours. The accounts run smoothly without any glitches, and the data analytics tools are top-notch, helping us optimize our ads in real time. Thanks for delivering such an amazing service!",
    user: "Daisy",
    role: "",
    avatar: avatar2  // 添加头像属性
  },
  {
    title: "Seamless Setup & Outstanding ROI Improvement",
    content: "I just have to say how impressed I am with your media ad accounts. The setup was seamless, the ad approval process is fast, and we're already getting way better ROI than we did with our previous provider. You've definitely got a long-term customer here!",
    user: "Steven",
    role: "",
    avatar: avatar3  // 添加头像属性
  },
  {
    title: "Hassle-Free Management & Prompt Support",
    content: "Your media ad accounts are a breeze to manage—no complicated steps or confusing menus at all. Whenever we run into a small issue, your team gets back to us in minutes, making our ad operations so much easier. We couldn't ask for a better partner!",
    user: "Philip",
    role: "",
    avatar: avatar4  // 添加头像属性
  },
  {
    title: "High Approval Rate & Target Audience Accuracy",
    content: "What really blows us away is the high approval rate of your ad accounts—our creatives get green-lit almost instantly. The audience targeting is also spot-on, which helps us reach exactly the users we want to convert. Great job!",
    user: "Eva",
    role: "",
    avatar: avatar5  // 添加头像属性
  },
  {
    title: "Stable Performance & Transparent Data Tracking",
    content: "These ad accounts have never let us down—they run stably even during peak advertising seasons. The data tracking is fully transparent too; we can check every metric clearly and make data-driven decisions without any hassle.",
    user: "Faith",
    role: "",
    avatar: avatar6  // 添加头像属性
  },
  {
    title: "Cost-Effective & High Conversion Efficiency",
    content: "Compared to other providers, your ad accounts offer unbeatable cost-effectiveness. We're spending less on ad budgets but getting way higher conversion rates, which has significantly boosted our overall marketing profits.",
    user: "Lewis",
    role: "",
    avatar: avatar7  // 添加头像属性
  }
])
// 响应式变量
const trackRef = ref(null)
const translateX = ref(0)
const isPlaying = ref(true)
const scrollSpeed = ref(1.5) // 优化滑动速度
const cardWidth = ref(380) // 匹配图片中的卡片宽度
const cardHeight = ref(380) // 匹配图片中的卡片高度
const gap = 20 // 卡片间距
const containerWidth = ref(0)

// 创建循环数组
const allComments = computed(() => {
  // 为了让滚动更平滑，复制数组以创建无缝循环
  return [...comments.value, ...comments.value, ...comments.value]
})

// 获取用户姓名首字母
const getInitials = (name) => {
  if (!name) return "?"
  return name.split(' ').map(n => n[0]).join('').toUpperCase()
}

// 自动滚动动画
let animationId = null
let lastTimestamp = 0

const animateScroll = (timestamp) => {
  if (!lastTimestamp) lastTimestamp = timestamp
  
  const elapsed = timestamp - lastTimestamp
  const delta = scrollSpeed.value * (elapsed / 16) // 基于60fps标准化
  
  if (isPlaying.value) {
    translateX.value -= delta
    
    // 计算总滚动宽度
    const totalScrollWidth = comments.value.length * (cardWidth.value + gap)
    
    // 当滑动距离达到一组卡片的宽度时，重置位置实现无缝循环
    if (Math.abs(translateX.value) >= totalScrollWidth) {
      translateX.value = 0
    }
  }
  
  lastTimestamp = timestamp
  animationId = requestAnimationFrame(animateScroll)
}

// 暂停自动滚动
const pauseAutoScroll = () => {
  isPlaying.value = false
}

// 恢复自动滚动
const resumeAutoScroll = () => {
  isPlaying.value = true
}

// 响应式调整
const handleResize = () => {
  if (trackRef.value?.parentElement) {
    containerWidth.value = trackRef.value.parentElement.clientWidth
    
    // 根据屏幕宽度调整卡片宽度
    if (window.innerWidth < 768) {
      // 移动端：卡片宽度为容器宽度减去内边距
      cardWidth.value = containerWidth.value - 40
      cardHeight.value = 360
    } else if (window.innerWidth < 1024) {
      // 平板端：两列布局
      cardWidth.value = (containerWidth.value - gap) / 2 - 20
      cardHeight.value = 370
    } else {
      // 桌面端：四列布局（如图片所示）
      cardWidth.value = 380
      cardHeight.value = 380
    }
  }
}

// 初始化
onMounted(() => {
  // 设置初始容器宽度
  handleResize()
  
  // 开始动画
  animationId = requestAnimationFrame(animateScroll)
  
  // 监听窗口大小变化
  window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
  if (animationId) {
    cancelAnimationFrame(animationId)
  }
  window.removeEventListener('resize', handleResize)
})
</script>

<style scoped>
.comments-carousel-container {
  background-color: #ffffff; /* 改为白色背景 */
  color: #1f2937; /* 改为深灰色文字 */
  padding: 60px 20px 40px; /* 这里可以调整下边距 */
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  overflow: hidden;
  position: relative;
  min-height: auto;
}

/* 滑动区域容器 */
.carousel-track-container {
  width: 100%;
  overflow: hidden;
  position: relative;
  background: transparent;
  margin: 0 auto;
  max-width: 1600px;
  padding: 20px 0;
}

/* 滑动轨道 */
.comments-track {
  display: flex;
  gap: 20px;
  will-change: transform;
  transition: transform 0.1s linear;
  padding: 10px 40px;
  width: max-content;
}

/* 评论卡片 - 适配白色背景 */
.comment-card {
  flex: 0 0 auto;
  width: 380px; /* 卡片宽度 */
  min-height: 380px; /* 卡片高度 */
  background: #f8fafc; /* 改为浅灰色背景适配白色主题 */
  border-radius: 12px;
  padding: 24px;
  position: relative;
  transition: all 0.3s ease;
  border: 1px solid rgba(209, 213, 219, 0.6); /* 改为浅灰色边框 */
  display: flex;
  flex-direction: column;
  align-items: flex-start; /* 整体左对齐 */
  text-align: left; /* 文本左对齐 */
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08); /* 改为浅色阴影 */
  overflow: hidden;
}

.comment-card:hover {
  transform: translateY(-2px);
  border-color: rgba(16, 185, 129, 0.3); /* 悬停时绿色边框 */
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
  background: #ffffff; /* 悬停时纯白色背景 */
}

/* 星级评分 - 绿色星星（保持不变） */
.rating {
  display: flex;
  gap: 4px;
  margin-bottom: 20px;
  justify-content: flex-start; /* 左对齐 */
}

.star-icon {
  color: #10b981; /* 绿色星星 */
  font-size: 1.3rem;
  opacity: 0.9;
}

/* 评论标题 - 适配白色背景 */
.comment-title {
  font-size: 1.0rem;
  font-weight: 700;
  margin-bottom: 25px;
  color: #1f2937; /* 改为深灰色 */
  line-height: 1.3;
  text-align: left; /* 左对齐 */
  width: 100%;
  letter-spacing: -0.3px;
  opacity: 0.95;
}

/* 评论内容 - 适配白色背景 */
.comment-content {
  color: #4b5563; /* 改为中灰色文字 */
  line-height: 1.6;
  font-size: 1.05rem;
  margin-bottom: 24px;
  flex-grow: 1;
  font-style: normal;
  text-align: left; /* 左对齐 */
  width: 100%;
  opacity: 0.8;
}

/* 用户信息 */
.user-info {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-top: auto;
  padding-top: 20px;
  border-top: 1px solid rgba(209, 213, 219, 0.5); /* 改为浅灰色分隔线 */
  width: 100%;
  justify-content: flex-start; /* 左对齐 */
}

.user-avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  position: relative;
  overflow: hidden;
  border: 2px solid #ffffff; /* 白色边框 */
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  background: #f3f4f6; /* 浅灰色背景作为fallback */
}

.avatar-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
}

.user-avatar::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transform: translateX(-100%);
  transition: transform 0.6s ease;
}

.comment-card:hover .user-avatar::before {
  transform: translateX(100%);
}

.user-avatar:hover {
  transform: scale(1.05);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.user-details {
  display: flex;
  flex-direction: column;
  gap: 2px;
  text-align: left; /* 左对齐 */
}

.user-name {
  font-weight: 600;
  font-size: 1rem;
  color: #1f2937; /* 改为深灰色 */
  margin: 0;
  letter-spacing: -0.2px;
  opacity: 0.95;
}

.user-role {
  font-size: 0.85rem;
  color: #6b7280; /* 改为中灰色 */
  margin: 0;
  opacity: 0.7;
}

/* 移动端适配 */
@media (max-width: 1023px) {
  .comments-carousel-container {
    padding: 40px 16px 30px;
  }
  
  .comment-card {
    min-height: 370px; /* 移动端调整高度 */
    padding: 20px;
    width: calc(50vw - 40px);
  }
  
  .carousel-track-container {
    padding: 20px 0;
  }
  
  .comment-title {
    font-size: 1.3rem;
  }
  
  .comment-content {
    font-size: 1rem;
    line-height: 1.6;
  }
  
  .comments-track {
    padding: 10px 20px;
  }
}

@media (max-width: 767px) {
  .comments-carousel-container {
    padding: 30px 12px 20px;
  }
  
  .comment-card {
    min-height: 360px;
    padding: 20px;
    width: calc(100vw - 40px);
    border-radius: 10px;
  }
  
  .comment-title {
    font-size: 1.2rem;
  }
  
  .comment-content {
    font-size: 0.95rem;
    line-height: 1.5;
  }
  
  .user-avatar {
    width: 40px;
    height: 40px;
  }
  
  .user-name {
    font-size: 1rem;
  }
  
  .user-role {
    font-size: 0.85rem;
  }
  
  .rating {
    margin-bottom: 16px;
  }
  
  .star-icon {
    font-size: 1.2rem;
  }
  
  .comments-track {
    gap: 16px;
    padding: 10px 20px;
  }
}

@media (max-width: 480px) {
  .comments-carousel-container {
    padding: 20px 8px 15px;
  }
  
  .comment-card {
    min-height: 320px; /* 进一步减小高度适应小屏幕 */
    width: calc(100vw - 24px);
    padding: 16px;
  }
  
  .comment-title {
    font-size: 1.1rem;
    margin-bottom: 15px;
  }
  
  .comment-content {
    font-size: 0.9rem;
    line-height: 1.4;
    margin-bottom: 20px;
  }
  
  .user-info {
    padding-top: 15px;
  }
  
  .user-avatar {
    width: 36px;
    height: 36px;
  }
  
  .user-name {
    font-size: 0.95rem;
  }
  
  .user-role {
    font-size: 0.8rem;
  }
  
  .comments-track {
    gap: 12px;
    padding: 10px 16px;
  }
  
  .rating {
    margin-bottom: 12px;
  }
  
  .star-icon {
    font-size: 1.1rem;
  }
}

/* 平板设备优化 */
@media (min-width: 768px) and (max-width: 1023px) {
  .comment-card {
    width: calc(50vw - 60px);
  }
  
  .comments-track {
    gap: 16px;
  }
}

/* 大屏幕优化 */
@media (min-width: 1400px) {
  .comments-carousel-container {
    padding: 80px 20px 60px;
  }
  
  .carousel-track-container {
    max-width: 1800px;
  }
}

/* 触摸设备优化 */
@media (hover: none) and (pointer: coarse) {
  .comment-card:hover {
    transform: none;
  }
  
  .comment-card:active {
    transform: translateY(-2px);
    background: #ffffff;
  }
}
</style>