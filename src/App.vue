<script setup>
import { ref } from 'vue'

const items = [
  { text: '"The only way to do great work is to love what you do." — Steve Jobs（做伟大工作的唯一方式是热爱你所做的事情。）"' },
  { text: '"Success is not final, failure is not fatal: It is the courage to continue that counts." — Winston Churchill（成功不是终点，失败不是致命的：重要的是继续前行的勇气。）'},
  { text: '"You miss 100% of the shots you don’t take." — Wayne Gretzky（你错过的每一次机会，都是你没抓住的100%的机会。）'},
  // 添加更多卡片数据...
]
const currentIndex = ref(0)
const startX = ref(0)
const offsetX = ref(0)
const isAnimating = ref(false)

function handleTouchStart(e) {
  isAnimating.value = false
  startX.value = e.touches[0].clientX
}

function handleTouchMove(e) {
  if (isAnimating.value) return
  const currentX = e.touches[0].clientX
  offsetX.value = currentX - startX.value
}

function handleTouchEnd() {
  if (isAnimating.value) return
  const threshold = window.innerWidth * 0.3

  if (Math.abs(offsetX.value) > threshold) {
    isAnimating.value = true
    if (offsetX.value > 0 && currentIndex.value > 0) {
      // 向右滑动
      currentIndex.value--
    } else if (offsetX.value < 0 && currentIndex.value < items.length - 1) {
      // 向左滑动
      currentIndex.value++
    }
  }

  offsetX.value = 0
  setTimeout(() => isAnimating.value = false, 300)
}
</script>

<template>
  <div class="container">
    <div class="card-wrapper" :style="{ 
        transform: `translateX(calc(${-currentIndex * 100}% + ${offsetX}px))`,
        transition: isAnimating ? 'transform 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94)' : 'none'
      }" @touchstart="handleTouchStart" @touchmove="handleTouchMove" @touchend="handleTouchEnd">
      <div v-for="(item, index) in items" :key="item.id" class="card">
        <h1>{{ item.text }}</h1>
      </div>
    </div>

    <!-- 分页指示器 -->
    <div class="pagination">
      <div v-for="n in items.length" :key="n" :class="['dot', { active: n-1 === currentIndex }]" />
    </div>
  </div>
</template>

<style scoped>
.container {
  position: relative;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

.card-wrapper {
  display: flex;
  height: 100%;
  will-change: transform;
}

.card {
  flex: 0 0 100%;
  width: 80%;
  height: 60%;
  margin: auto;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s, box-shadow 0.3s;
  color: black;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  user-select: none;
}

.pagination {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 8px;
}

.dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.5);
  transition: all 0.3s;
}

.dot.active {
  width: 20px;
  border-radius: 4px;
  background: rgba(255, 255, 255, 0.9);
}

/* 美化卡片内容 */
h1 {
  font-size: 2.5em;
  margin-bottom: 20px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}

</style>