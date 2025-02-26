<script setup>
import { ref, onMounted } from "vue";

// 包含 HTML 字符串的数组
const text = [
  {
    chinese: "早八人通勤：当代人类丧尸化实录🚇🧟♂️",
    english: "Dawn patrol commuters: Modern zombies with coffee IV drips",
    detail:
      "【dawn patrol /dɔːn pəˈtroʊl/ 清晨巡逻队】、【zombies /ˈzɑmbiz/ 丧尸】、【IV drips /aɪ vi drɪps/ 静脉注射】",
    explain: "将打工人早高峰比喻成丧尸电影，咖啡续命像医疗急救，荒诞又真实",
  },
  {
    chinese: "健身房自拍：人类新型光合作用💪📸",
    english: "Gym selfies: Photosynthesis for social validation",
    detail:
      "【photosynthesis /ˌfoʊtoʊˈsɪnθəsɪs/ 光合作用】、【validation /ˌvælɪˈdeɪʃən/ 认可】",
    explain: "用植物生存原理类比健身晒照求点赞，揭露现代社交本质",
  },
  {
    chinese: "通勤耳机：社畜的精神防空洞🎧🕳️",
    english: "Noise-canceling headphones: Corporate trench warfare armor",
    detail:
      "【trench warfare /trɛntʃ ˈwɔrˌfɛr/ 堑壕战】、【armor /ˈɑrmər/ 盔甲】",
    explain: "把降噪耳机比作战场装备，夸张表现打工人通勤生存状态",
  },
  {
    chinese: "周末补觉：打工人的人体充电工程💤🔋",
    english: "Weekend hibernation: Biological battery recharge protocol",
    detail:
      "【hibernation /ˌhaɪbərˈneɪʃən/ 冬眠】、【protocol /ˈproʊtəˌkɑːl/ 协议】",
    explain: "将睡觉科技术语化，制造程序设定般的疲惫生活既视感",
  },
  {
    chinese: "网购购物车：月光族的量子存钱罐🛒🌗",
    english: "Digital cart therapy: Schrödollinger's savings paradox",
    detail: "【paradox /ˈpærəˌdɑks/ 悖论】、【therapy /ˈθɛrəpi/ 治疗】",
    explain: "融合量子物理概念，调侃「加购=已拥有」的当代消费幻觉",
  },
  {
    chinese: "奶茶续杯：打工人液态多巴胺补给🧋💉",
    english: "Bubble tea transfusions: Office dopamine booster shots",
    detail:
      "【transfusions /trænsˈfjuʒənz/ 输血】、【dopamine /ˈdoʊpəˌmin/ 多巴胺】",
    explain: "用医疗术语包装奶茶依赖症，幽默揭示职场提神秘籍",
  },
  {
    chinese: "表情包斗图：赛博时代的甲骨文战争🦁💬",
    english: "Emoji warfare: Hieroglyphic battles in cyberspace",
    detail:
      "【hieroglyphic /ˌhaɪərəˈɡlɪfɪk/ 象形文字】、【cyberspace /ˈsaɪbərˌspeɪs/ 网络空间】",
    explain: "将表情包对比远古文字，制造文明传承的错位幽默感",
  },
  {
    "chinese": "键盘战士的元宇宙起义⌨️🦸♂️",
    "english": "Keyboard warriors: Cyberspace revolution in pajamas",
    "detail": "【cyberspace /ˈsaɪbərˌspeɪs/ 网络空间】、【revolution /ˌrɛvəˈluʃən/ 革命】、【pajamas /pəˈdʒɑməz/ 睡衣】",
    "explain": "把网络吐槽升格为虚拟世界革命，睡衣装备突显宅家作战的反差萌"
  },
  {
    "chinese": "午休趴桌：打工人的系统重置💤🔄",
    "english": "Desk naps: BIOS reboot for overclocked humans",
    "detail": "【BIOS /ˈbaɪɒs/ 基本输入输出系统】、【overclocked /ˌoʊvərˈklɑkt/ 超频的】",
    "explain": "用电脑术语包装午睡，暗示打工人如同需要维护的机器"
  },
  {
    "chinese": "奶茶测评：液态甜品考古学🧋⛏️",
    "english": "Bubble tea connoisseurs: Modern liquid paleontology",
    "detail": "【connoisseurs /ˌkɑnəˈsɜrz/ 鉴赏家】、【paleontology /ˌpeɪliɑnˈtɑlədʒi/ 古生物学】",
    "explain": "将喝奶茶比作考古研究，调侃当代青年「挖料」的仪式感"
  },
  {
    "chinese": "地铁占座：打工人原始本能觉醒🚇🦍",
    "english": "Seat hunting: Office primates' territorial instinct",
    "detail": "【primates /ˈpraɪmeɪts/ 灵长类】、【territorial /ˌtɛrɪˈtɔriəl/ 领地意识】",
    "explain": "用动物世界比喻抢座大战，揭示职场人的生存竞争本质"
  },
  {
    "chinese": "撤回消息：社死患者的时光机⏪🚑",
    "english": "Message recall: Emergency temporal paradox fixer",
    "detail": "【temporal /ˈtɛmpərəl/ 时间的】、【paradox /ˈpærəˌdɑks/ 悖论】",
    "explain": "将撤回功能科幻化，比喻成抢救社交死亡的时光倒流装置"
  },
  {
    "chinese": "深夜emo：当代青年情感焚化炉🎶🔥",
    "english": "Midnight melancholia: Emotional waste incineration",
    "detail": "【melancholia /ˌmɛlənˈkoʊliə/ 忧郁症】、【incineration /ɪnˌsɪnəˈreɪʃən/ 焚烧】",
    "explain": "把网抑云时间比作垃圾处理，黑色幽默化解情绪内耗"
  },
  {
    "chinese": "扫码点餐：社恐人士的无接触求生📱🛡️",
    "english": "QR code ordering: Social anxiety force field",
    "detail": "【force field /fɔrs fild/ 力场】、【anxiety /æŋˈzaɪəti/ 焦虑】",
    "explain": "用物理防护概念包装扫码功能，精准戳中社恐痛点"
  },
  {
    "chinese": "追星打投：粉丝经济学货币战争🌟💹",
    "english": "Fandom voting: Emotional stock market manipulation",
    "detail": "【fandom /ˈfændəm/ 粉丝圈】、【manipulation /məˌnɪpjʊˈleɪʃən/ 操控】",
    "explain": "将追星行为金融化，揭露粉丝经济背后的资本游戏"
  },
  {
    "chinese": "空气炸锅：厨房黑洞物质生成器🍟🌀",
    "english": "Air fryer alchemy: Dark matter culinary edition",
    "detail": "【alchemy /ˈælkəmi/ 炼金术】、【culinary /ˈkʌlɪˌnɛri/ 烹饪的】",
    "explain": "用科幻概念包装厨房神器，调侃「万物皆可炸」的神秘"
  },
  {
    "chinese": "综艺追更：打工人精神透析疗程📺💊",
    "english": "Variety show marathons: Psychological dialysis sessions",
    "detail": "【dialysis /daɪˈæləsɪs/ 透析】、【psychological /ˌsaɪkəˈlɑdʒɪkəl/ 心理的】",
    "explain": "将追综艺比作医疗行为，幽默揭示当代人的解压刚需"
  }
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

      <div class="chinese-box">
        <p class="chinese-text">{{ read.chinese }}</p>
      </div>

      <div class="detail-box">
        <p class="detail-text">{{ read.detail }}</p>
      </div>

      <div class="english-box">
        <p class="english-text">{{ read.english }}</p>
      </div>

      <div class="explain-box">
        <p class="explain-text">{{ read.explain }}</p>
      </div>
    </div>
    <button class="refresh-btn" @click="refresh">✨ 灵感刷新</button>
  </div>
</template>

<style scoped>
.containerA {
  max-width: 100vw;
  background: white;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.content-box {
  background: white;
  border: 1px solid #e9ecef;
}


.chinese-box {
  padding: 0.5rem;
  background: white;
  border: 1px solid #e9ecef;
  border-left: 4px solid #74b9ff;
}

.chinese-text {
  margin-top: 2rem;
  color: #2d3436;
  font-size: 1.5rem;
  line-height: 1.4;
  padding-left: 1rem;
}

.explain-box {
  padding: 0.5rem;
  background: white;
  border: 1px solid #e9ecef;
  border-left: 4px solid sienna;
}

.explain-text {
  color: #2d3436;
  font-size: 1.5rem;
  line-height: 1.4;
  padding-left: 1rem;
}

.english-box {
  padding: 0.5rem;
  background: white;
  border: 1px solid #e9ecef;
  border-left: 4px solid lightcoral;
}

.english-text {
  color: black;
  font-size: 1.6rem;
  line-height: 1.2;
  padding-left: 1rem;
}

.detail-box {
  padding: 0.5rem;
  background: white;
  border: 1px solid #e9ecef;
  border-left: 4px solid lightseagreen;
}

.detail-text {
  color: #2d3436;
  font-size: 1.5rem;
  padding: 0.5rem;
  background: white;
  line-height: 1.3;
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