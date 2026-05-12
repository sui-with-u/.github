<p align="center">
  <img src="https://raw.githubusercontent.com/sui-with-u/.github/main/profile/banner.jpg" width="366">
</p>

<h3 align="center">"夜来南风起，小麦覆陇黄"</h3>
<h5 align="center">"With the night came a southern breeze; the wheat now blankets the ridges in gold."</h5>
<h3 align="center">「穗」，象征着丰收与希望，麦穗黄、九穗嘉禾。</h3>
<h5 align="center">「穗」the ear of grain — symbolizes harvest and hope: the golden hue of ripening wheat, and the auspicious nine-eared grain.</h5>

<p align="center">
  <a href="#-sui-生态--sui-ecosystem">生态 Ecology</a> ·
  <a href="#-仓库--repositories">仓库 Repositories</a> ·
  <a href="#-架构--architecture">架构 Architecture</a> ·
  <a href="#-引擎--engines">引擎 Engines</a> ·
  <a href="#-license">许可证 License</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-building-7C3AED?style=flat-square" alt="status">
  <img src="https://img.shields.io/badge/license-PolyForm%20Noncommercial-3B82F6?style=flat-square" alt="license">
  <img src="https://img.shields.io/badge/language-TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="typescript">
  <img src="https://img.shields.io/badge/runtime-Bun-F9F1E1?style=flat-square&logo=bun&logoColor=black" alt="bun">
  <img src="https://img.shields.io/badge/frontend-React-61DAFB?style=flat-square&logo=react&logoColor=black" alt="react">
</p>

---

<details>
<summary><b>🇨🇳 中文</b></summary>

<br>

## 🌾 Sui 生态 · Sui Ecosystem

**SuiBot** 是一个基于大语言模型（LLM）的模块化拟人化 AI 智能体。名称取自汉字 **「穗」**（suì），象征丰收与希望。

她不是普通的聊天机器人。SuiSui 拥有**情感、记忆与会随时间演化的性格**——她会因为你的话语而高兴或低落，会记住你们之间发生过的事，也会在漫长的陪伴中逐渐形成自己独特的样子。

生态采用**主仓库 + 独立扩展仓库**方案：

```
suibot/  ← 主仓库（Core + Engines + Manager，无 WebUI 可独立运行）
├── core/               ← 核心大脑
├── engines/            ← 四个引擎（情感/记忆/审视/优先级）
├── tools/
│   ├── tool-manager/   ← Tool Manager（内置）
│   └── tools/          ← 外部 Tool 落地目录（按需拉取）
└── hands/
    ├── hand-manager/   ← Hand Manager（内置）
    └── hands/          ← 外部 Hand 落地目录（Manager 拉取，不进版本控制）

独立仓库（H-* / T-*），通过命令行或 WebUI 按需安装：
H-SuiWeb · H-OneBot · H-Telegram · H-Minecraft · T-TTS · T-Weather …
```

> **一个主仓库 + 按需拉取的 Hand/Tool = 完整的 SuiSui 生态**

---

## 📦 仓库 · Repositories

### 主仓库 & 基础设施

| 仓库 | 说明 | 状态 |
|------|------|------|
| [suibot](https://github.com/sui-with-u/suibot) | 主仓库：Core + Engines + Manager，标准部署的全部内容 | 🚧 开发中 |
| [SuiStd](https://github.com/sui-with-u/SuiStd) | 项目编码规范、最终愿景与开发路径 | 🚧 开发中 |
| [SuiFw](https://github.com/sui-with-u/SuiFw) | Bun + TypeScript 7 后端脚手架，配置好的空项目模板，供团队学习与快速开始 | 🚧 开发中 |
| [.github](https://github.com/sui-with-u/.github) | 组织主页、Issue 模板、许可证 | 🚧 维护中 |

### Hand 仓库（`H-` 前缀）

| 仓库 | 说明 | 状态 |
|------|------|------|
| [H-SuiWeb](https://github.com/sui-with-u/H-SuiWeb) | 管理面板，情感曲线可视化、记忆查询、参数配置 | 🚧 开发中 |
| [H-SuiDevWeb](https://github.com/sui-with-u/H-SuiDevWeb) | 开发调试面板 | 🚧 开发中 |
| [H-OneBot](https://github.com/sui-with-u/H-OneBot) | QQ 双向消息（NapCat） | 📌 待开发 |
| [H-Telegram](https://github.com/sui-with-u/H-Telegram) | Telegram 机器人 | 📌 待开发 |
| [H-Minecraft](https://github.com/sui-with-u/H-Minecraft) | Minecraft 聊天 / 指令 / 自动化 | 📌 待开发 |

### Tool 仓库（`T-` 前缀）

| 仓库 | 说明 | 状态 |
|------|------|------|
| [T-TTS](https://github.com/sui-with-u/T-TTS) | 语音合成（Text-to-Speech） | 📌 待开发 |
| [T-Weather](https://github.com/sui-with-u/T-Weather) | 天气查询 | 📌 待开发 |
| [T-Calendar](https://github.com/sui-with-u/T-Calendar) | 日历与提醒 | 📌 待开发 |

---

## 🏗 架构 · Architecture

SuiBot 采用**类冯·诺依曼半阻塞总线流**——一次只处理一件事，行为更贴近真实人类。

```
┌──────────────────────────────────────────────────────────────┐
│                       外部层  HANDS                           │
│   独立仓库（H-*），落地在 hands/hands/，各自独立运行          │
│                                                              │
│  H-SuiWeb   H-OneBot   H-Telegram   H-Minecraft   ...       │
└───────────────────────────┬──────────────────────────────────┘
                            │ WebSocket
┌───────────────────────────▼──────────────────────────────────┐
│              HAND MANAGER（hands/hand-manager/）              │
│   WS 连接管理 · 优先级委托 Priority Engine                    │
│   独立管理外部 Hand 仓库的拉取 / 注册 / 启停                  │
└───────────────────────────┬──────────────────────────────────┘
                            │
┌───────────────────────────▼──────────────────────────────────┐
│                      SUICORE（core/）                         │
│   ① 接收 → ② 查引擎 → ③ 组Prompt → ④ LLM → ⑤ 决策分发      │
│                                          ↙            ↘      │
│                                     直接回复        调Tool   │
└──────┬──────────────┬─────────────┬────────────┬─────────────┘
       ↓              ↓             ↓            ↓  Core 直接调用，无 Manager
  ┌─────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐
  │ Emotion │  │  Memory  │  │ Reflect  │  │ Priority │
  │ Engine  │  │  Engine  │  │ Engine   │  │ Engine   │
  │PAD情感  │  │Buffer+VDB│  │审视→Prompt│  │优先级路由│
  └─────────┘  └──────────┘  └──────────┘  └──────────┘
       ↑ 引擎层 ENGINES（engines/）
┌──────────────────────────────────────────────────────────────┐
│                       扩展层  TOOLS                           │
│   tools/tool-manager/  独立管理外部 Tool 仓库的拉取/启停      │
│   tools/tools/         外部 Tool 落地目录（T-TTS、T-Weather…）│
└──────────────────────────────────────────────────────────────┘
```

### 部署说明

```bash
# 标准部署（只需主仓库，WebUI 也是外部 Hand，按需安装）
git clone https://github.com/sui-with-u/suibot
cd suibot && bun install && bun run start

# 所有拉取 / 启停必须经过 Core 指令触发，由对应 Manager 执行
# CLI / WebUI → Core → Hand Manager / Tool Manager → 操作
# Manager 可自行处理简单的本层事务（心跳、断线重连、超时重试），无需经过 Core

bun run sui add H-SuiWeb        # 拉取并安装（Manager 在 sui-with-u 下搜索同名仓库）
bun run sui start H-SuiWeb      # 启动
bun run sui stop H-SuiWeb       # 停止
bun run sui add T-TTS           # Tool 同理
```

---

## ✨ 引擎 · Engines

SuiSui 的「有温度」来自四个引擎，由 Core 直接调用：

### 🎭 Emotion Engine · PAD 情感引擎

基于 **PAD 三维情感模型**（Mehrabian & Russell, 1974）：

| 维度 | 含义 | 正值 | 负值 |
|------|------|------|------|
| **P** Pleasure 愉悦度 | 主观感受 | 开心、满足 | 难过、失落 |
| **A** Arousal 激活度 | 兴奋程度 | 激动、兴奋 | 疲惫、平静 |
| **D** Dominance 支配度 | 掌控感 | 自信、主动 | 被动、顺从 |

情绪**指数衰减**回稳态，每次对话叠加**情感波动向量**。

### 🧠 Memory Engine · 记忆引擎

基于**艾宾浩斯遗忘曲线**：

- **短期 Buffer**：最近 5~10 轮，保障实时连贯
- **长期 VectorDB**（ChromaDB）：语义检索 + 自然遗忘 + 记忆混淆

### 🌱 Reflect Engine · 自我审视引擎

每 10 条消息或每天 23:00 触发，读取近期情感曲线和核心记忆，生成自我描述并注入下次对话的 System Prompt。性格从经历中缓慢涌现，而非写死的固定模板。

### ⚡ Priority Engine · 优先级引擎

管理消息优先级队列（PPP / P0 / P1 / P2 / P3）和路由规则，由 Hand Manager 委托调用，与其他引擎同级。

---

## 📡 通信协议 · Protocol

所有 Hand ↔ Core 通信统一 **WebSocket + JSON**：

```json
{
  "type": "input | output | status | command | error",
  "from": "hand_name",
  "to": "core | hand_name | null",
  "payload": { "action": "...", "...": "..." },
  "priority": "PPP | P0 | P1 | P2 | P3",
  "msg_id": "uuid-v4",
  "timestamp": 1712345678,
  "version": "1.0"
}
```

完整规范见 [PROTOCOL.md](https://github.com/sui-with-u/suibot/blob/main/PROTOCOL.md)。

---

## 🛠 技术栈 · Tech Stack

| 层 | 技术 |
|----|------|
| 语言 | TypeScript 7 Beta |
| 运行时 | Bun |
| 前端 | React + Vite + ShadCN UI + Recharts |
| 向量数据库 | ChromaDB |
| LLM | DeepSeek API（可替换） |
| 通信 | WebSocket + JSON |

---

## 📜 License

Copyright (c) 2026 Sui-With-u

本组织下所有仓库均使用 **PolyForm Noncommercial License 1.0.0** 许可，仅允许**非商业用途**。

详见 [LICENSE](https://github.com/sui-with-u/.github/blob/main/LICENSE) 文件。

---

</details>

<details>
<summary><b>🇬🇧 English</b></summary>

<br>

## 🌾 Sui Ecosystem

**SuiBot** is a modular, LLM-powered humanized AI agent. Its name comes from the Chinese character **「穗」** (suì), symbolizing harvest and hope.

She is not an ordinary chatbot. SuiSui has **emotion, memory, and a personality that evolves over time** — she feels happy or sad in response to what you say, remembers things that happened between you, and gradually becomes her own person through your interactions.

The ecosystem uses a **main repo + independent extension repos** approach:

```
suibot/  ← main repo (Core + Engines + Managers, runs without WebUI)
├── core/               ← Core brain
├── engines/            ← Four engines (Emotion/Memory/Reflect/Priority)
├── tools/
│   ├── tool-manager/   ← Tool Manager (built-in)
│   └── tools/          ← External Tool landing dir (pulled on demand)
└── hands/
    ├── hand-manager/   ← Hand Manager (built-in)
    └── hands/          ← External Hand landing dir (pulled by Manager, git-ignored)

Independent repos (H-* / T-*), installed via CLI or WebUI:
H-SuiWeb · H-OneBot · H-Telegram · H-Minecraft · T-TTS · T-Weather …
```

> **One main repo + on-demand Hand/Tool = the complete SuiSui ecosystem**

---

## 📦 Repositories

### Main Repository & Infrastructure

| Repository | Description | Status |
|------------|-------------|--------|
| [suibot](https://github.com/sui-with-u/suibot) | Main repo: Core + Engines + Managers, everything needed for standard deployment | 🚧 Building |
| [SuiStd](https://github.com/sui-with-u/SuiStd) | Project coding standards, final vision & development roadmap | 🚧 Building |
| [SuiFw](https://github.com/sui-with-u/SuiFw) | Bun + TypeScript 7 backend scaffold — a pre-configured empty project for team learning and quick starts | 🚧 Building |
| [.github](https://github.com/sui-with-u/.github) | Organization profile, Issue templates, license | 🚧 Active |

### Hand Repositories (`H-` prefix)

| Repository | Description | Status |
|------------|-------------|--------|
| [H-SuiWeb](https://github.com/sui-with-u/H-SuiWeb) | Management dashboard: emotion visualization, memory search, config | 🚧 Building |
| [H-SuiDevWeb](https://github.com/sui-with-u/H-SuiDevWeb) | Developer debug panel | 🚧 Building |
| [H-OneBot](https://github.com/sui-with-u/H-OneBot) | QQ bidirectional messaging (NapCat) | 📌 Planned |
| [H-Telegram](https://github.com/sui-with-u/H-Telegram) | Telegram bot | 📌 Planned |
| [H-Minecraft](https://github.com/sui-with-u/H-Minecraft) | Minecraft chat / commands / automation | 📌 Planned |

### Tool Repositories (`T-` prefix)

| Repository | Description | Status |
|------------|-------------|--------|
| [T-TTS](https://github.com/sui-with-u/T-TTS) | Text-to-Speech synthesis | 📌 Planned |
| [T-Weather](https://github.com/sui-with-u/T-Weather) | Weather lookup | 📌 Planned |
| [T-Calendar](https://github.com/sui-with-u/T-Calendar) | Calendar and reminders | 📌 Planned |

---

## 🏗 Architecture

SuiBot uses a **Von Neumann-inspired semi-blocking bus flow** — one thing at a time, just like a real person.

```
┌──────────────────────────────────────────────────────────────┐
│                       EXTERNAL  HANDS                         │
│   Independent repos (H-*), landed in hands/hands/            │
│                                                              │
│  H-SuiWeb   H-OneBot   H-Telegram   H-Minecraft   ...       │
└───────────────────────────┬──────────────────────────────────┘
                            │ WebSocket
┌───────────────────────────▼──────────────────────────────────┐
│                HAND MANAGER (hands/hand-manager/)             │
│   WS connection lifecycle · routing via Priority Engine       │
│   Independently manages external Hand repo pull/start/stop   │
└───────────────────────────┬──────────────────────────────────┘
                            │
┌───────────────────────────▼──────────────────────────────────┐
│                      SUICORE (core/)                          │
│  ① Recv → ② Query → ③ Prompt → ④ LLM → ⑤ Dispatch          │
│                                        ↙             ↘       │
│                                  Direct Reply      Call Tool  │
└──────┬──────────────┬─────────────┬────────────┬─────────────┘
       ↓              ↓             ↓            ↓  direct call, no Manager
  ┌─────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐
  │ Emotion │  │  Memory  │  │ Reflect  │  │ Priority │
  │ Engine  │  │  Engine  │  │ Engine   │  │ Engine   │
  │PAD model│  │Buffer+VDB│  │→ Prompt  │  │Routing   │
  └─────────┘  └──────────┘  └──────────┘  └──────────┘
       ↑ ENGINES layer (engines/)
┌──────────────────────────────────────────────────────────────┐
│                         TOOLS                                 │
│   tools/tool-manager/  manages external Tool repo pull/start │
│   tools/tools/         external Tool landing dir             │
└──────────────────────────────────────────────────────────────┘
```

### Deployment

```bash
# Standard deployment (WebUI is also an external Hand, installed on demand)
git clone https://github.com/sui-with-u/suibot
cd suibot && bun install && bun run start

# All install / start / stop commands must go through Core → Manager
# CLI / WebUI → Core → Hand Manager / Tool Manager → action
# Managers may handle simple local tasks (heartbeat, reconnect, timeout retry) without Core

bun run sui add H-SuiWeb        # pull & install (Manager searches sui-with-u org)
bun run sui start H-SuiWeb      # start
bun run sui stop H-SuiWeb       # stop
bun run sui add T-TTS           # same for Tools
```

---

## ✨ Engines

SuiSui's warmth comes from four engines, called directly by Core:

### 🎭 Emotion Engine · PAD Model

Based on the **PAD three-dimensional emotion model** (Mehrabian & Russell, 1974):

| Dimension | Meaning | Positive | Negative |
|-----------|---------|----------|----------|
| **P** Pleasure | Subjective feeling | Happy, satisfied | Sad, lost |
| **A** Arousal | Excitement level | Excited, energetic | Tired, calm |
| **D** Dominance | Sense of control | Confident, assertive | Passive, submissive |

Emotions **decay exponentially** back to baseline; each conversation adds a **delta vector**.

### 🧠 Memory Engine · Layered Memory

Inspired by the **Ebbinghaus Forgetting Curve**:

- **Short-term Buffer**: Last 5–10 turns, real-time coherence
- **Long-term VectorDB** (ChromaDB): semantic retrieval + natural forgetting + memory interference

### 🌱 Reflect Engine · Personality Evolution

Triggered every 10 messages or at 23:00 daily. Reads recent emotion curves and core memories, generates a self-description, injects it into the next System Prompt. Personality emerges from experience — not a fixed template.

### ⚡ Priority Engine · Message Routing

Manages the priority queue (PPP / P0 / P1 / P2 / P3) and routing rules. Delegated by Hand Manager, same level as other engines.

---

## 📡 Protocol

All Hand ↔ Core communication uses **WebSocket + JSON**:

```json
{
  "type": "input | output | status | command | error",
  "from": "hand_name",
  "to": "core | hand_name | null",
  "payload": { "action": "...", "...": "..." },
  "priority": "PPP | P0 | P1 | P2 | P3",
  "msg_id": "uuid-v4",
  "timestamp": 1712345678,
  "version": "1.0"
}
```

Full specification: [PROTOCOL.md](https://github.com/sui-with-u/suibot/blob/main/PROTOCOL.md)

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|------------|
| Language | TypeScript 7 Beta |
| Runtime | Bun |
| Frontend | React + Vite + ShadCN UI + Recharts |
| Vector DB | ChromaDB |
| LLM | DeepSeek API (swappable) |
| Transport | WebSocket + JSON |

---

## 📜 License

Copyright (c) 2026 Sui-With-u

All repositories in this organization are licensed under the **PolyForm Noncommercial License 1.0.0**.
You may use, modify, and distribute the software for **noncommercial purposes only**.

See the [LICENSE](https://github.com/sui-with-u/.github/blob/main/LICENSE) file for details.

---

</details>

<br>

<p align="center">
  <sub>穗穗碎碎念 · Sui-With-u</sub>
</p>
