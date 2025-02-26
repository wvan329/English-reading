<script setup>
import { ref, onMounted } from "vue";

// 包含 HTML 字符串的数组
const text = [
  {
    chinese:
      "拖延症不是懒，是大脑在等待最佳量子波动时机 ⚛️（树獭教我的效率哲学）",
    detail:
      "量子波动→quantum fluctuation [ˈkwɑːntəm ˌflʌk.tʃuˈeɪ.ʃən] / 树獭隐喻→sloth-sama（日语尊称）式学习法",
    english:
      "Procrastination isn't laziness—it's your brain waiting for the perfect quantum moment! 🌱 (Sloths process information at 0.3x speed but 300% accuracy)",
  },
  {
    chinese: "已读不回是人类最古老的通信礼仪——鸽子送信时也从不写回执 📜",
    detail:
      "通信礼仪→communication etiquette [kəˌmjuːnɪˈkeɪʃən ˈetɪket] / 历史梗：古埃及信使被已读不回会被罚建造迷你金字塔",
    english:
      "'Seen 3:14PM' is the modern hieroglyph for 'I'll respond when the Nile floods again' 🌊",
  },
  {
    chinese: "松鼠式焦虑：囤了365天外卖优惠券却找不到人一起用 🐿️",
    detail:
      "松鼠式→squirrel mode [ˈskwɜːrəl moʊd] / 行为经济学：hoarding mentality in digital age",
    english:
      "Digital hoarding disorder: Saving 200+ food coupons just in case the raccoon apocalypse comes 🦝 (Expiry date: Before loneliness does)",
  },
  {
    chinese: "通勤地铁是当代人类唯一合法的瞬移体验——虽然方向永远固定 🚇",
    detail:
      "瞬移→teleportation [ˌtelɪpɔːrˈteɪʃən] / 科幻梗：《星际迷航》传送装置≈地铁闸机",
    english:
      "Subways are government-approved teleporters that only transport you to capitalist wonderlands 💼 (Warning: May occasionally materialize in meetings)",
  },
  {
    chinese: "午睡时流的口水是大脑CPU的液态散热系统 💤",
    detail:
      "液态散热→liquid cooling [ˈlɪkwɪd ˈkuːlɪŋ] / 计算机隐喻：REM sleep=系统碎片整理",
    english:
      "Naptime drool = Your biological liquid cooling system in action! ❄️ (Overclocking your neurons for 3PM Zoom battles)",
  },
  {
    chinese: "外卖软件是潘多拉魔盒——每次打开都放出热量恶魔和贫穷精灵 🍱",
    detail:
      "潘多拉魔盒→Pandora's app [pænˈdɔːrəz æp] / 希腊神话现代版：优惠券=希望之糖",
    english:
      "Food delivery apps: Digital Pandora's boxes that unleash calorie demons and budget goblins 👾 (Hopes remain in ￥15 off coupons)",
  },
  {
    chinese: "自动回复「嗯嗯」的脑电波频率=微波炉完成加热时的「叮」🔊",
    detail: "脑电波→brainwave [ˈbreɪnweɪv] / 声学双关：'mmm'≈微波炉提示音",
    english:
      "Replying 'mmhmm' activates the same brain frequency as microwaving leftovers 🍛 (Cognitive ready-to-serve status)",
  },
  {
    chinese: "追剧时流泪不是脆弱——是瞳孔在给心灵做盐水SPA 🛁",
    detail: "盐水SPA→brine therapy [braɪn ˈθerəpi] / 医学伪概念：眼泪排毒指数",
    english:
      "Crying over K-dramas isn't weakness—it's ocular detoxification with plot twists! 🌊 (Tear salinity level indicates emotional investment)",
  },
  {
    chinese: "多肉植物是佛系青年的电子宠物——每周浇水就像给手机充电 🌵",
    detail:
      "电子宠物→digital pet [ˈdɪdʒɪtl pet] / 世代特征：植物=不会已读不回的理想室友",
    english:
      "Succulents are millennials' tamagotchi: Watering them weekly = Charging your soul 🔋 (Overwatering error: Root rot blues)",
  },
  {
    chinese: "天气预报「30%降水概率」= 老天爷的抽奖游戏 ☔",
    detail:
      "抽奖游戏→lottery system [ˈlɑːtəri ˈsɪstəm] / 行为学：人类带伞行为≈购买后悔保险",
    english:
      "30% chance of rain = Sky's loot box where umbrellas are the pity timer 🌦️ (Epic drop: Unexpected rainbow)",
  },
];

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
  <div class="containerA">
    <div class="content-box">
      <h2 class="chinese-text">{{ read.chinese }}</h2>
      <p class="detail-text">{{ read.detail }}</p>
      <div class="english-box">
        <p class="english-text">{{ read.english }}</p>
      </div>
    </div>
    <button class="refresh-btn" @click="refresh">✨ 灵感刷新</button>
  </div>
</template>

<style scoped>
.containerA {
  max-width: 100vw;
  /* margin: 2rem auto; */
  /* padding: 2rem; */
  background: #f8f9fa;
  /* border-radius: 15px; */
  /* box-shadow: 0 10px 30px rgba(0,0,0,0.1); */
}

.content-box {
  background: white;
  /* padding: 2rem; */
  border-radius: 12px;
  border: 1px solid #e9ecef;
}

.chinese-text {
  color: #2d3436;
  font-size: 1.8rem;
  line-height: 1.4;
  /* margin-bottom: 1.5rem; */
  border-left: 4px solid #74b9ff;
  padding-left: 1rem;
}

.detail-text {
  color: #6c757d;
  font-size: 0.95rem;
  margin: 1.2rem 0;
  padding: 1rem;
  background: #f1f3f5;
  border-radius: 8px;
  line-height: 1.6;
}

.english-box {
  margin-top: 2rem;
  padding: 1.5rem;
  background: #fff9f0;
  border-radius: 8px;
  border: 1px solid #ffe8cc;
}

.english-text {
  color: #495057;
  font-size: 1.1rem;
  line-height: 1.6;
  white-space: pre-wrap;
}

.refresh-btn {
  display: block;
  width: 200px;
  margin: 2rem auto 0;
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

@media (max-width: 768px) {
  .container {
    margin: 1rem;
    padding: 1.5rem;
  }

  .chinese-text {
    font-size: 1.4rem;
  }
}
</style>