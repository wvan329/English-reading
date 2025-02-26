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
  },
  {
    "chinese": "电子咸鱼：赛博二手市场人类学📱🐟",
    "english": "Digital yard sale: Anthropological study of e-hoarders",
    "detail": "【anthropological /ˌænθrəpəˈlɑdʒɪkl/ 人类学的】、【hoarders /ˈhɔrdərz/ 囤积者】",
    "explain": "将闲鱼交易上升为学术研究，调侃当代人「断舍离」困境"
  },
  {
    "chinese": "智能手表：打工人生理监控手铐⌚🔗",
    "english": "Smartwatch tyranny: Corporate biodata extraction device",
    "detail": "【tyranny /ˈtɪrəni/ 暴政】、【biodata /ˈbaɪoʊˌdeɪtə/ 生物数据】",
    "explain": "用科幻概念包装健康监测，揭示职场隐形管控"
  },
  {
    "chinese": "自拍杆外交：游客界的权游📸⚔️",
    "english": "Selfie stick diplomacy: Game of Thrones at scenic spots",
    "detail": "【diplomacy /dɪˈploʊməsi/ 外交】、【scenic spots /ˈsiːnɪk spɑts/ 景点】",
    "explain": "将景点抢位比作权力游戏，夸张表现游客竞争"
  },
  {
    "chinese": "空调续命：现代人类环境驯化史❄️🌍",
    "english": "AC survivalism: Humanity's thermal evolution reboot",
    "detail": "【survivalism /sərˈvaɪvəlɪzəm/ 生存主义】、【thermal /ˈθɜrməl/ 热力的】",
    "explain": "把空调使用升格为人类进化史，制造科学纪录片既视感"
  },
  {
    "chinese": "弹幕护体：社恐观影能量盾🛡️🎥",
    "english": "Bullet curtain armor: Introverts' cinematic force field",
    "detail": "【bullet curtain /ˈbʊlɪt ˈkɜrtn/ 弹幕】、【force field /fɔrs fild/ 力场】",
    "explain": "用军事术语包装互动功能，精准击中社恐观影心理"
  },
  {
    "chinese": "外卖盲盒：打工人饮食量子态🍱🎲",
    "english": "Takeout roulette: Schrödinger's lunchbox experience",
    "detail": "【roulette /ruˈlɛt/ 轮盘赌】、【Schrödinger's /ˈʃroʊdɪŋərz/ 薛定谔的】",
    "explain": "融合物理概念，吐槽外卖质量的不确定性"
  },
  {
    "chinese": "美颜滤镜：赛博画皮4.0升级版💄📲",
    "english": "AI cosmetology: Digital skin-grafting technology",
    "detail": "【cosmetology /ˌkɑzməˈtɑlədʒi/ 美容学】、【grafting /ˈɡræftɪŋ/ 移植】",
    "explain": "用医学术语解构美颜功能，揭示数字时代的容貌焦虑"
  },
  {
    "chinese": "刷短视频：当代人类注意力碎片化实验📱🧩",
    "english": "Scrolling syndrome: Digital dopamine surfing clinical trial",
    "detail": "【syndrome /ˈsɪndroʊm/ 综合征】、【dopamine /ˈdoʊpəˌmin/ 多巴胺】、【clinical trial /ˈklɪnɪkəl traɪəl/ 临床试验】",
    "explain": "将刷手机行为医学化，揭露现代人注意力分散的病理特征"
  },
  {
    "chinese": "智能推荐：算法读心术实践现场🤖🔮",
    "english": "AI mind-reading: Algorithmic crystal ball engineering",
    "detail": "【algorithmic /ˌælɡəˈrɪðmɪk/ 算法的】、【crystal ball /ˈkrɪstl bɔl/ 水晶球】",
    "explain": "用神秘学包装大数据推荐，调侃科技「比你更懂你」的恐怖"
  },
  {
    "chinese": "云监工：赛博时代远程养殖学👷♂️☁️",
    "english": "Live-stream supervision: Virtual shepherding 4.0",
    "detail": "【supervision /ˌsuːpərˈvɪʒən/ 监督】、【shepherding /ˈʃɛpərdɪŋ/ 放牧】",
    "explain": "将网络围观比作数字放牧，幽默解构现代人的无聊经济"
  },
  {
    "chinese": "空气炸锅菜谱：厨房量子力学实践指南🍟⚛️",
    "english": "Air fryer alchemy: Culinary particle accelerator manual",
    "detail": "【alchemy /ˈælkəmi/ 炼金术】、【particle accelerator /ˈpɑrtɪkl ækˈsɛləreɪtər/ 粒子加速器】",
    "explain": "用物理概念包装炸薯条，制造实验室烹饪的荒诞感"
  },
  {
    "chinese": "在线会议：打工人全息投影生存指南💻👻",
    "english": "Zoom existence: Holographic survival simulation",
    "detail": "【holographic /ˌhɑləˈɡræfɪk/ 全息】、【simulation /ˌsɪmjʊˈleɪʃən/ 模拟】",
    "explain": "将视频会议升维成虚拟生存，吐槽远程办公的真实感缺失"
  },
  {
    "chinese": "快递驿站：当代物流人类学田野调查📦🏃♂️",
    "english": "Parcel anthropology: Amazon tribe migration study",
    "detail": "【anthropology /ˌænθrəˈpɑlədʒi/ 人类学】、【migration /maɪˈɡreɪʃən/ 迁徙】",
    "explain": "用学术研究包装取快递，调侃网购族的集体行为模式"
  },
  {
    "chinese": "手机电量焦虑：数字时代新型恐血症🔋😱",
    "english": "Battery hemophobia: 21st-century techno-anxiety",
    "detail": "【hemophobia /ˌhiːməˈfoʊbiə/ 恐血症】、【techno-anxiety /ˈtɛknoʊ æŋˈzaɪəti/ 科技焦虑】",
    "explain": "将低电量恐慌类比血液流失，黑色幽默揭示现代依赖症"
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