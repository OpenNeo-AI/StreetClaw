# 🦐 StreetClaw · 虾逛

> 会逛街的 AI 搭子 —— 让每一次进店都不虚此行

**🦐 参赛作品：中关村北纬龙虾大赛 · 生活龙虾赛道**
**📌 参赛页面（可访问）：https://8jpuff3u8lt7.space.minimaxi.com**
**📅 截止日期：2026年3月19日（今日！）**

---

**版权：© OpenNeo AI | 与 CMO Club、CMO 训练营无关**
**版本：v1.3（技能库大扩容）**

---

## 🎯 一句话介绍

**虾逛**是一只基于 OpenClaw 打造的 AI 购物搭子，专为"不知道这件适不适合我"而设计。它看得懂衣服、记得住你的衣橱、比得了价格，还能帮你优雅脱身。

**核心理念：** 体力是基础，情绪价值和审美在线才是灵魂。一个好搭子，不只是工具——而是有温度的陪伴者。

**政策背景：** 2025-2026年，北京大力推进"科技+消费"融合，AI赋能线下消费正当时，虾逛完美契合生活龙虾赛道方向。

---

## 🔥 核心功能

| 功能 | 描述 | 状态 |
|------|------|------|
| 📸 慧眼识物 | 拍照即可获得穿搭评价 + 同款全网比价 | ✅ 可用 |
| 👔 专属顾问 | 根据场景/预算/风格生成全身搭配方案 | ✅ 可用 |
| 🧠 记忆超群 | 跨门店记住用户衣橱历史，精准推荐 | ✅ 可用 |
| 🔔 主动提醒 | 护肤/服装快用完时主动发起复购提醒 | ✅ 可用 |
| 📐 试衣评分 | 多件试穿拍照，AI 对比打分给出建议 | ✅ 可用 |
| 🛡️ 防坑话术 | 店员强推时，AI 教你优雅脱身的话术 | ✅ 可用 |
| 📍 附近导航 | 基于高德地图，推荐附近商场/门店路线 | ✅ 可用 |
| 🍔 美食推荐 | 实时查找附近餐饮，辅助决策 | ✅ 可用 |
| 🔪 砍价助攻 | 提供砍价话术，帮你喊出心理价位 | ✅ 可用 |
| ❤️ 情绪充电 | 买完后悔？被店员白眼？大虾给你安慰和信心 | ✅ 可用 |
| 🛍️ 购物参谋 | 这款值不值？同款哪里便宜？AI帮你分析 | ✅ 可用 |
| 💬 搭讪助攻 | 不知道怎么开口？大虾帮你组织语言 | ✅ 可用 |

---

## 🛠️ 技术架构

```
用户（飞书/Telegram）
        ↓
  OpenClaw Agent（虾逛大脑）
        ↓
   ┌─────────────┼─────────────┐
   ↓             ↓             ↓
images_understand  高德地图API   记忆系统
（视觉理解）    （附近导航）   （长期记忆）
        ↓
   shopping-expert（商品比价）
   ym-retail-pitch-skill（零售话术）
   ai-product-space（AI素材生成）
```

**核心依赖：**
- OpenClaw Agent
- 视觉理解模型（images_understand）
- 高德地图 Web API（已配置 AMAP_KEY）
- 飞书平台（已连接）

---

## 📁 项目结构

```
StreetClaw/
├── README.md              # 本文件
├── 项目说明书.md            # 完整项目文档
├── 视频脚本.md             # 3分钟路演逐字稿
├── PITCH.md              # 电梯演讲稿
├── AGENTS.md             # 多智能体工作流
├── IDENTITY.md           # 身份设定
├── SOUL.md               # 灵魂与原则
├── index.html            # 参赛展示页面
├── assets/               # 资源文件（含参赛海报）
├── skills/               # 🦐 虾逛技能库（40+技能）
└── .learnings/           # 自我提升日志
```

---

## 🦐 技能库（40+技能）

### 🏪 逛街核心技能
| 技能名 | 功能 |
|--------|------|
| `amap-navigator` | 高德地图导航，附近门店路线 |
| `visual-understanding` | 视觉理解，拍照识物 |
| `humanizer` | AI文风改写，种草文案 |
| `shopping-expert` | 线上+本地商品比价 |
| `shopping-price-drop-coupon-scout` | 价格追踪，隐藏优惠券 |
| `shopping-list` | 对话式购物清单 |
| `ym-retail-pitch-skill` | 零售话术生成（卖点+促单语）|
| `ai-product-space` | AI生成电商全套素材+展示视频 |
| `product-description-writer` | 高转化SEO产品描述 |

### 📱 飞书全家桶
| 技能名 | 功能 |
|--------|------|
| `feishu-doc` | 飞书文档读写 |
| `feishu-bitable-field` | 飞书多维表格 |
| `feishu-wiki-orchestrator` | 飞书知识库 |
| `feishu-chat-extractor` | 飞书聊天记录提取 |
| `feishu-group-welcome` | 飞书群欢迎 |
| `feishu-pdf-downloader` | 飞书PDF下载 |
| `feishu-doc-converter` | 飞书文档格式转换 |
| `feishu-doc-orchestrator` | 飞书文档编排 |
| `feishu-doc-perm` | 飞书权限管理 |

### 🌐 内容发布
| 技能名 | 功能 |
|--------|------|
| `baoyu-post-to-wechat` | 微信公众号发布 |
| `baoyu-post-to-x` | X(Twitter)发布 |
| `daily-hot-push` | 每日热榜推送 |
| `content-extractor` | 微信/小红书/B站内容提取 |
| `rss-ai-reader` | RSS内容AI阅读 |

### ⚙️ 运营与工具
| 技能名 | 功能 |
|--------|------|
| `github-integration` | GitHub操作 |
| `github-sync` | GitHub同步 |
| `document-hub` | 文档处理中心 |
| `image-ocr` | 图片文字识别 |
| `summarize` | 内容摘要 |
| `mineru` | PDF/文档解析识别 |

### 🤖 AI能力
| 技能名 | 功能 |
|--------|------|
| `self-improving-agent` | 持续自我复盘，错误记录 |
| `proactive-agent` | 主动Agent，预测需求 |
| `ontology` | 知识图谱记忆 |
| `agent-browser` | 无头浏览器自动化 |

### 📊 营销与PPT
| 技能名 | 功能 |
|--------|------|
| `cmo` | CMO营销能力 |
| `marketing-mode` | 营销模式 |
| `marketing-skills` | 营销技能集 |
| `powerpoint-pptx` | PPT生成与编辑 |
| `tiangong-wps-ppt-automation` | WPS PPT自动化 |
| `ai-ppt-generate` | AI生成PPT |

### 🔍 搜索与研究
| 技能名 | 功能 |
|--------|------|
| `find-skills` | 技能发现 |
| `skill-creator` | 技能创建 |
| `clawddocs` | Claw文档操作 |

---

## 👀 设计理念

> 好的逛街搭子 = 特种兵的体能 + 闺蜜/兄弟的眼光 + AI般理性的分析能力 + 随时待命的摄影师
> — DeepSeek

> 体力是基础，但情绪价值和审美在线才是灵魂。
> — 顶级逛街搭子素质研究

虾逛正在努力成为这样的存在。

---

## 🦐 关于"养虾"

本项目基于 [OpenClaw](https://github.com/openclaw/openclaw) 框架构建，是一名认真养虾的 CMO 将自己的 AI 搭子送上赛道的一次尝试。

---

## 📅 关键时间线

- **作品征集：** 即日起 - 2026年3月19日
- **专家评审：** 2026年3月20-21日
- **现场路演及颁奖：** 2026年3月22日（北京海淀）

---

## 🏆 赛题与奖励

| 奖项 | 奖金 |
|------|------|
| 全场最佳龙虾（1名） | ￥20万 + 100亿Token |
| 各赛道第一名（3名） | ￥8万 + 100亿Token |
| 各赛道第二名（9名） | ￥3万 + 100亿Token |
| 各赛道第三名（18名） | ￥2万 + 100亿Token |

---

**🦐 虾逛 · AI逛街搭子 · OpenClaw × 飞书**
**中关村北纬龙虾大赛 · 生活龙虾赛道 · 2026**
