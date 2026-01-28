// 忍野忍角色类
class ShinobuOshino {
  constructor() {
    // 基础属性
    this.name = "忍野忍";
    this.trueName = "姬丝秀忒·雅赛劳拉莉昂·刃下心";
    this.age = 598;
    this.height = 127; // cm
    this.weight = null; // 秘密
    
    // 状态属性
    this.form = "幼女形态";
    this.energy = 100;
    this.donutsConsumed = 0;
    this.isInShadow = true;
    
    // 能力等级
    this.abilities = {
      regeneration: 5,
      strength: 4,
      speed: 5,
      shadowManipulation: 4,
      energyAbsorption: 5,
      matterCreation: 3
    };
    
    // 关系
    this.master = "阿良良木历";
    this.relationships = {
      "阿良良木历": "主人/眷属",
      "忍野咩咩": "命名者",
      "战场原黑仪": "同伴",
      "羽川翼": "同伴"
    };
    
    // 甜甜圈偏好
    this.donutPreferences = {
      favorite: "蜂蜜 glaze",
      dailyGoal: 10,
      favoriteShop: "Mister Donut"
    };
  }
  
  // 形态变换方法
  transform(targetForm) {
    const validForms = ["幼女形态", "中间形态", "完全体"];
    
    if (!validForms.includes(targetForm)) {
      console.log(`无法变形成 ${targetForm}！`);
      return false;
    }
    
    this.form = targetForm;
    
    // 根据形态调整能力
    switch(targetForm) {
      case "完全体":
        this.abilities.strength = 10;
        this.abilities.speed = 10;
        this.abilities.regeneration = 10;
        this.height = 180;
        break;
      case "中间形态":
        this.abilities.strength = 7;
        this.abilities.speed = 7;
        this.abilities.regeneration = 7;
        this.height = 155;
        break;
      case "幼女形态":
        this.abilities.strength = 4;
        this.abilities.speed = 5;
        this.abilities.regeneration = 5;
        this.height = 127;
        break;
    }
    
    console.log(`${this.name} 变身为 ${targetForm}！`);
    return true;
  }
  
  // 消耗甜甜圈
  consumeDonut(type = "蜂蜜 glaze", quantity = 1) {
    this.donutsConsumed += quantity;
    this.energy += quantity * 10;
    
    if (this.energy > 100) this.energy = 100;
    
    console.log(`${this.name} 吃了 ${quantity} 个 ${type} 甜甜圈！`);
    console.log(`今日甜甜圈摄入: ${this.donutsConsumed}`);
    console.log(`当前能量: ${this.energy}%`);
    
    // 检查是否达成每日目标
    if (this.donutsConsumed >= this.donutPreferences.dailyGoal) {
      console.log("🎯 达成每日甜甜圈目标！");
    }
    
    return this.energy;
  }
  
  // 使用能力
  useAbility(abilityName, target = null) {
    const abilityCosts = {
      regeneration: 15,
      shadowManipulation: 20,
      energyAbsorption: 25,
      matterCreation: 30
    };
    
    if (!this.abilities[abilityName]) {
      console.log(`${this.name} 无法使用 ${abilityName} 能力！`);
      return false;
    }
    
    const cost = abilityCosts[abilityName] || 10;
    
    if (this.energy < cost) {
      console.log(`能量不足！需要 ${cost}，当前只有 ${this.energy}`);
      return false;
    }
    
    this.energy -= cost;
    
    const abilityActions = {
      regeneration: () => {
        console.log("💫 高速再生启动中...");
        return "伤势已恢复";
      },
      shadowManipulation: () => {
        console.log("🌑 影子操纵中...");
        this.isInShadow = !this.isInShadow;
        return this.isInShadow ? "潜入影子" : "脱离影子";
      },
      energyAbsorption: (target) => {
        console.log(`🔋 从${target || "目标"}吸收能量中...`);
        this.energy += 30;
        if (this.energy > 100) this.energy = 100;
        return `能量恢复至 ${this.energy}%`;
      },
      matterCreation: (item) => {
        console.log(`✨ 创造${item || "物品"}中...`);
        return `${item || "物品"}创造完成`;
      }
    };
    
    const result = abilityActions[abilityName]
      ? abilityActions[abilityName](target)
      : "能力发动！";
    
    console.log(`能力使用成功: ${result}`);
    console.log(`剩余能量: ${this.energy}%`);
    
    return result;
  }
  
  // 与阿良良木历互动
  interactWithMaster(action) {
    const interactions = {
      "抱怨": "吾肚子饿了，给吾买甜甜圈。",
      "感谢": "哼，这次就谢谢你了。",
      "战斗": "要战斗吗？让吾来保护你。",
      "日常": "今天也要一起去买甜甜圈吗？"
    };
    
    const response = interactions[action] || 
      `吾是汝的${this.name}，汝是吾的${this.master}。`;
    
    console.log(`${this.name}: "${response}"`);
    return response;
  }
  
  // 显示状态面板
  showStatus() {
    console.log(`
╔══════════════════════════════════════╗
║        忍野忍 - 状态面板            ║
╠══════════════════════════════════════╣
║ 形态：${this.form.padEnd(16)}年龄：${this.age}岁    ║
║ 能量：${this.energy}%${" ".repeat(15)}主人：${this.master}║
║ 甜甜圈：${this.donutsConsumed}个${" ".repeat(13)}身高：${this.height}cm  ║
╠══════════════════════════════════════╣
║            能力等级                  ║
║  再生：${"★".repeat(this.abilities.regeneration)}${"☆".repeat(5-this.abilities.regeneration)}    ║
║  力量：${"★".repeat(this.abilities.strength)}${"☆".repeat(5-this.abilities.strength)}    ║
║  速度：${"★".repeat(this.abilities.speed)}${"☆".repeat(5-this.abilities.speed)}    ║
║  影子：${"★".repeat(this.abilities.shadowManipulation)}${"☆".repeat(5-this.abilities.shadowManipulation)}    ║
╚══════════════════════════════════════╝
    `);
    
    return {
      form: this.form,
      energy: this.energy,
      donuts: this.donutsConsumed,
      abilities: this.abilities
    };
  }
  
  // 显示经典语录
  static getQuotes() {
    return [
      "吾乃忍野忍，曾为吸血鬼，现为阿良々木暦之眷属。",
      "吾不是说过吗？吾是汝的忍野忍，汝是吾的阿良良木历。",
      "甜甜圈...再给吾一个。",
      "吸血鬼的弱点？那种东西，不过是人类的一厢情愿罢了。",
      "吾活了598年，什么没见过？"
    ];
  }
}

// 忍野忍的时间线类
class ShinobuTimeline {
  constructor() {
    this.events = [
      { year: -598, event: "诞生于欧洲", era: "吸血鬼时期" },
      { year: -400, event: "获得'怪异杀手'称号", era: "吸血鬼时期" },
      { year: 2005, event: "被吸血鬼猎人重伤，与阿良良木历相遇", era: "现代" },
      { year: 2006, event: "成为忍野忍，开始现代日本生活", era: "现代" },
      { year: "现在", event: "住在阿良良木家的影子中", era: "现代" }
    ];
  }
  
  displayTimeline() {
    console.log("\n忍野忍的时间线：");
    console.log("=".repeat(40));
    
    this.events.forEach(event => {
      console.log(`[${event.year}年] ${event.event} (${event.era})`);
    });
  }
}

// 甜甜圈管理系统
class DonutManager {
  constructor(owner) {
    this.owner = owner;
    this.inventory = [];
    this.dailyLog = [];
    this.totalConsumed = 0;
  }
  
  addDonut(type, shop = "Mister Donut") {
    const donut = {
      type: type,
      shop: shop,
      timestamp: new Date(),
      id: Math.random().toString(36).substr(2, 9)
    };
    
    this.inventory.push(donut);
    console.log(`🍩 获得 ${type} 甜甜圈 (来自 ${shop})`);
    
    return donut;
  }
  
  consumeDonut(donutId) {
    const index = this.inventory.findIndex(d => d.id === donutId);
    
    if (index === -1) {
      console.log("找不到指定的甜甜圈！");
      return null;
    }
    
    const donut = this.inventory.splice(index, 1)[0];
    this.dailyLog.push(donut);
    this.totalConsumed++;
    
    console.log(`🍽️ 吃掉 ${donut.type} 甜甜圈`);
    
    // 记录消耗时间
    const now = new Date();
    donut.consumedAt = now;
    
    return donut;
  }
  
  getDailyStats() {
    const today = new Date().toDateString();
    const todayDonuts = this.dailyLog.filter(d => 
      new Date(d.consumedAt).toDateString() === today
    );
    
    const stats = {
      totalToday: todayDonuts.length,
      byType: {},
      byShop: {}
    };
    
    todayDonuts.forEach(donut => {
      stats.byType[donut.type] = (stats.byType[donut.type] || 0) + 1;
      stats.byShop[donut.shop] = (stats.byShop[donut.shop] || 0) + 1;
    });
    
    console.log(`\n📊 今日甜甜圈统计:`);
    console.log(`总计: ${stats.totalToday} 个`);
    console.log(`按类型:`, stats.byType);
    console.log(`按店铺:`, stats.byShop);
    
    return stats;
  }
}

// 能力可视化组件（HTML/CSS）
const createAbilityChartHTML = () => `
<style>
.ability-chart {
  font-family: 'Arial', sans-serif;
  background: linear-gradient(135deg, #2c003e 0%, #4a148c 100%);
  color: white;
  padding: 20px;
  border-radius: 15px;
  max-width: 400px;
  margin: 20px auto;
}

.ability-bar {
  margin: 15px 0;
}

.ability-name {
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

.bar-container {
  height: 20px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  overflow: hidden;
}

.bar-fill {
  height: 100%;
  background: linear-gradient(90deg, #ff4081 0%, #ff79b0 100%);
  border-radius: 10px;
  transition: width 1s ease;
}

.donut-counter {
  background: rgba(255, 215, 0, 0.2);
  padding: 15px;
  border-radius: 10px;
  margin-top: 20px;
  text-align: center;
}

.quote-box {
  font-style: italic;
  border-left: 4px solid #ff4081;
  padding-left: 15px;
  margin-top: 20px;
  color: #e1bee7;
}
</style>

<div class="ability-chart">
  <h2>忍野忍能力面板</h2>
  
  <div class="ability-bar">
    <div class="ability-name">
      <span>再生能力</span>
      <span>★★★★★</span>
    </div>
    <div class="bar-container">
      <div class="bar-fill" style="width: 100%"></div>
    </div>
  </div>
  
  <div class="ability-bar">
    <div class="ability-name">
      <span>速度</span>
      <span>★★★★★</span>
    </div>
    <div class="bar-container">
      <div class="bar-fill" style="width: 100%"></div>
    </div>
  </div>
  
  <div class="ability-bar">
    <div class="ability-name">
      <span>影子操纵</span>
      <span>★★★★☆</span>
    </div>
    <div class="bar-container">
      <div class="bar-fill" style="width: 80%"></div>
    </div>
  </div>
  
  <div class="donut-counter">
    <h3>🍩 今日甜甜圈: 8/10</h3>
    <progress value="8" max="10"></progress>
  </div>
  
  <div class="quote-box">
    "吾乃忍野忍，曾为吸血鬼，现为阿良々木暦之眷属。"
  </div>
</div>
`;

// 演示使用示例
const demoShinobuSystem = () => {
  console.log("=== 忍野忍角色系统演示 ===\n");
  
  // 创建忍野忍实例
  const shinobu = new ShinobuOshino();
  
  // 显示初始状态
  shinobu.showStatus();
  
  // 消耗甜甜圈
  console.log("\n--- 甜甜圈时间 ---");
  shinobu.consumeDonut("蜂蜜 glaze", 3);
  shinobu.consumeDonut("巧克力", 2);
  
  // 使用能力
  console.log("\n--- 能力演示 ---");
  shinobu.useAbility("regeneration");
  shinobu.useAbility("shadowManipulation");
  
  // 形态变换
  console.log("\n--- 形态变换 ---");
  shinobu.transform("完全体");
  shinobu.showStatus();
  
  // 与主人互动
  console.log("\n--- 与阿良良木历互动 ---");
  shinobu.interactWithMaster("抱怨");
  shinobu.interactWithMaster("感谢");
  
  // 显示时间线
  const timeline = new ShinobuTimeline();
  timeline.displayTimeline();
  
  // 显示语录
  console.log("\n--- 经典语录 ---");
  const quotes = ShinobuOshino.getQuotes();
  quotes.forEach((quote, index) => {
    console.log(`${index + 1}. "${quote}"`);
  });
  
  // 甜甜圈管理演示
  console.log("\n--- 甜甜圈管理系统 ---");
  const donutManager = new DonutManager(shinobu);
  donutManager.addDonut("蜂蜜 glaze", "Mister Donut");
  donutManager.addDonut("草莓味", "Mister Donut");
  donutManager.getDailyStats();
};

// 执行演示
demoShinobuSystem();

// React组件示例（概念）
const ShinobuReactComponent = () => {
  return `
import React, { useState } from 'react';

const ShinobuCard = () => {
  const [form, setForm] = useState('幼女形态');
  const [energy, setEnergy] = useState(100);
  const [donuts, setDonuts] = useState(0);
  
  const forms = [
    { id: 1, name: '幼女形态', description: '通常状态' },
    { id: 2, name: '中间形态', description: '成长过程' },
    { id: 3, name: '完全体', description: '传说中的吸血鬼' }
  ];
  
  const eatDonut = () => {
    setDonuts(donuts + 1);
    setEnergy(Math.min(100, energy + 10));
  };
  
  return (
    <div className="shinobu-card">
      <h2>忍野忍角色卡片</h2>
      <div className="current-form">当前形态: {form}</div>
      <div className="energy-bar">
        能量: <progress value={energy} max="100"></progress>
      </div>
      <div className="donut-counter">
        甜甜圈: {donuts}个
        <button onClick={eatDonut}>吃甜甜圈</button>
      </div>
      <div className="form-selector">
        {forms.map(f => (
          <button key={f.id} onClick={() => setForm(f.name)}>
            {f.name}
          </button>
        ))}
      </div>
    </div>
  );
};

export default ShinobuCard;
  `;
};

// 导出模块（Node.js/ES6）
export { ShinobuOshino, ShinobuTimeline, DonutManager };
export default ShinobuOshino;

// 单元测试示例
const testShinobuSystem = () => {
  const shinobu = new ShinobuOshino();
  
  // 测试初始化
  console.assert(shinobu.name === "忍野忍", "名字初始化失败");
  console.assert(shinobu.age === 598, "年龄初始化失败");
  console.assert(shinobu.form === "幼女形态", "形态初始化失败");
  
  // 测试甜甜圈消耗
  const initialEnergy = shinobu.energy;
  shinobu.consumeDonut("蜂蜜 glaze");
  console.assert(shinobu.energy > initialEnergy, "甜甜圈能量恢复失败");
  
  // 测试形态变换
  shinobu.transform("完全体");
  console.assert(shinobu.form === "完全体", "形态变换失败");
  console.assert(shinobu.abilities.strength === 10, "完全体力量设置失败");
  
  // 测试能力使用
  shinobu.energy = 100;
  const result = shinobu.useAbility("regeneration");
  console.assert(shinobu.energy < 100, "能力消耗能量失败");
  
  console.log("所有测试通过！");
};

// 运行测试
testShinobuSystem();
