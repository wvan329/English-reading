<script setup>
import { ref, onMounted } from "vue";
// import fileContent from 'D:/Documents/python_project/pytorch/read.json';
import fileContent from "./assets/read2.json";

// 包含 HTML 字符串的数组
const text = fileContent;

const read = ref("");


const refresh = () => {
  const randomIndex = Math.floor(Math.random() * text.length);
  read.value = text[randomIndex];
};

// 组件挂载时选择随机元素
onMounted(() => {
  refresh();
});

</script>
<template>
  <div class="container">

    <div class="sentence-box">
      <div class="originC-text">{{read.originE}}</div>
      <div class="originC-text">{{read.originC}}</div>
      <div class="sentence-text">"{{ read.sentence }}"</div>
    </div>

    <div class="chinese-box">
      <div class="chinese-text">{{read.chinese}}</div>
    </div>

    <div class="note-box">
      <div class="note-text" v-for="(item,index) in read.note" :key="index">
        *{{item}}
      </div>
    </div>

    <div class="add-box">
      <div class="add-text">{{read.add}}</div>
    </div>

    <button class="refresh-btn" @click="refresh">✨ 灵感刷新</button>
  </div>
</template>

<style scoped>
.container {
  background: white;
  box-shadow: 0 10px 30px rgba(173, 173, 159, 0.947);
  min-height: 100vh; /* 确保容器至少充满整个视窗 */
  padding-bottom: 100px; /* 为按钮留出空间，避免内容被遮挡 */
}

.sentence-box {
  background: white;
  border: 1px solid #e9ecef;
  border-left: 6px solid lightcoral;
  padding-top: 0.5rem;
  padding-left: 1rem;
  padding-bottom: 0.5rem;
}

.sentence-text {
  padding-top: 1rem;
  color: black;
  font-size: 1.3rem;
  line-height: 1.4;
  /* padding: 0.5rem; */
}

.chinese-box {
  background: white;
  border: 1px solid #e9ecef;
  border-left: 6px solid #74b9ff;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  padding-left: 1rem;
}

.chinese-text {
  color: #2d3436;
  line-height: 1.5;
  font-size: 1.2rem;
  padding-right: 0.2rem;
}

.color {
  color: #9f272c;
  font-weight: 700;
}

.note-box {
  padding: 0.5rem;
  background: white;
  border: 1px solid #e9ecef;
  border-left: 6px solid lightseagreen;

  padding-left: 1rem;
}

.note-text {
  color: #2d3436;
  font-size: 1.2rem;
  line-height: 1.2;
  padding: 0.1rem;
}

.add-box {
  padding: 0.5rem;
  background: white;
  border: 1px solid #e9ecef;
  padding-left: 1rem;
}

.refresh-btn {
  position: fixed; /* 固定定位 */
  bottom: 20px; /* 距离底部20px */
  left: 50%; /* 水平居中 */
  transform: translateX(-50%);
  display: block;
  width: 200px;
  margin: 0rem auto 0;
  padding: 1rem 2rem;
  background: #3d8bdb;
  color: white;
  border: none;
  border-radius: 50px;
  font-size: 1.1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(116, 185, 255, 0.3);
}
</style>