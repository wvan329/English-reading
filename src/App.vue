<script setup>
import { ref, onMounted } from "vue";
// import fileContent from 'D:/Documents/python_project/pytorch/read.json';
import fileContent from './assets/read.json';

// 包含 HTML 字符串的数组
const text = fileContent


const read = ref("");

const refresh = () => {
  const randomIndex = Math.floor(Math.random() * text.length);
  read.value = text[randomIndex];
};

// 组件挂载时选择随机元素
onMounted(() => {
  if (text.length > 0) {
    const randomIndex = Math.floor(Math.random() * text.length);
    read.value = text[randomIndex];
  }
});
</script>
<template>
  <div class="container">

    <div class="sentence-box">
      <div class="topic-text">{{read.topic}}</div>
      <div class="sentence-text">"{{ read.sentence }}"</div>
    </div>

    <div class="translation-box">
      <div class="translation-text" v-for="(item,index) in read.translation" :key="index">
        <div v-if="index%2==1">{{item}}</div>
        <div v-else class="color">{{item}}</div>
      </div>
    </div>

    <div class="knowledge-box">
      <div class="knowledge-text" v-for="(item,index) in read.knowledge" :key="index">
        *{{item}}
      </div>
    </div>

    <button class="refresh-btn" @click="refresh">✨ 灵感刷新</button>
  </div>
</template>

<style scoped>
.container {
  background: white;
  box-shadow: 0 10px 30px rgba(173, 173, 159, 0.947);
}

.sentence-box {
  background: white;
  border: 1px solid #e9ecef;
  border-left: 6px solid lightcoral;
  padding-left: 1rem;
  padding-bottom: 0.5rem;
}

.topic-text {
  padding-top: 1.5rem;
  color: black;
  font-size: 1.4rem;
  line-height: 0.8;
}

.sentence-text {
  padding-top: 1rem;
  color: black;
  font-size: 1.3rem;
  line-height: 1.4;
  /* padding: 0.5rem; */
}

.translation-box {
  background: white;
  border: 1px solid #e9ecef;
  border-left: 6px solid #74b9ff;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  padding-left: 1rem;
}

.translation-text {
  color: #2d3436;
  line-height: 1.5;
  font-size: 1.2rem;
  padding-right: 0.2rem;
}

.color {
  color: #9f272c;
  font-weight: 700;
}

.knowledge-box {
  padding: 0.5rem;
  background: #e9ecef;
  border: 1px solid #e9ecef;
  border-left: 6px solid lightseagreen;

  padding-left: 1rem;
}

.knowledge-text {
  color: #2d3436;
  font-size: 1.2rem;
  background: #e9ecef;
  line-height: 1.2;
  padding: 0.1rem;
}

.refresh-btn {
  display: block;
  width: 200px;
  margin: 0rem auto 0;
  padding: 1rem 2rem;
  background: #74b9ff;
  color: white;
  border: none;
  border-radius: 50px;
  font-size: 1.1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(116, 185, 255, 0.3);
}

.refresh-btn:hover {
  background: #3d8bdb;
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(116, 185, 255, 0.5);
}
</style>