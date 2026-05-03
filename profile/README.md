<p align="center">
  <img src="https://raw.githubusercontent.com/sui-with-u/.github/main/profile/banner.jpg" width="400">
</p>

<h3 align="center">“夜来南风起，小麦覆陇黄”</h3>
<h5 align="center">“With the night came a southern breeze; the wheat now blankets the ridges in gold.”</h4>
<h3 align="center">「穗」，象征着丰收与希望，麦穗黄、九穗嘉禾。</h3>
<h5 align="center">「穗」the ear of grain—symbolizes harvest and hope: the golden hue of ripening wheat, and the auspicious nine-eared grain.</h4>

<p align="center">
  <a href="#-sui-生态">生态Ecology</a> ·
  <a href="#-repositories">仓库Repositories</a> ·
  <a href="#-architecture">架构Architecture</a> ·
  <a href="#-license">许可证License</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-building-7C3AED?style=flat-square" alt="status">
  <img src="https://img.shields.io/badge/license-PolyForm%20Noncommercial-3B82F6?style=flat-square" alt="license">
  <img src="https://img.shields.io/badge/language-Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="python">
</p>

<!-- Language Switcher -->

<details>
<summary><b>🇨🇳 中文</b></summary>

<br>

## 🌾 Sui 生态

**SuiBot** 是一个模块化的 AI 角色生态。名称取自汉字 **「穗」**（suì），象征丰收与希望。

它由两个层次构成：

| 层次 | 说明 |
|------|------|
| **核心（Core）** | 大脑。内置技能（LLM / TTS / OCR / STT）+ 情感 / 记忆 / 性格引擎 |
| **猫爪（Hands）** | 独立仓库，每个连接一个外部平台，通过 WebSocket 与 Core 通信 |

> 一个 SuiCore + 超多猫爪 = SuiBot 生态

---

## 📦 Repositories

| 仓库 | 说明 | 状态 |
|------|------|------|
| [SuiBot](https://github.com/sui-with-u/SuiBot) | 主仓库，生态总览与文档 | 🚧 开发中 |
| [SuiCore](https://github.com/sui-with-u/SuiCore) | 核心大脑，内置技能，WebSocket 服务端 | 🚧 开发中 |
| [SuiWeb](https://github.com/sui-with-u/SuiWeb) | 管理面板，可视化与数据管理 | 🚧 开发中 |
| [Sui2NapCatQQ](https://github.com/sui-with-u/Sui2NapCatQQ) | QQ 双向消息（NapCat 中间件） | 📌 待开发 |
| [Sui2vtuber](https://github.com/sui-with-u/Sui2vtuber) | VTubeStudio 皮套控制 | 📌 待开发 |
| [Sui2tg](https://github.com/sui-with-u/Sui2tg) | Telegram 机器人 | 📌 待开发 |
| [Sui2minecraft](https://github.com/sui-with-u/Sui2minecraft) | Minecraft 聊天 / 指令 / 自动化 | 📌 待开发 |

---

## 🏗 架构

```
                         ┌──────────────┐
                         │   SuiCore    │
                         │  ┌─────────┐ │
               ┌─────────┤  │ 技能    │ │
               │         │  │ ┌─────┐ │ │
               │         │  │ │ LLM │ │ │
               │         │  │ ├─────┤ │ │
               │         │  │ │ TTS │ │ │
               │ WS      │  │ ├─────┤ │ │
          ┌────┴─────┐   │  │ │ OCR │ │ │
          │  SuiWeb  │   │  │ ├─────┤ │ │
          └──────────┘   │  │ │ STT │ │ │
                         │  │ └─────┘ │ │
          ┌──────────┐   │  └─────────┘ │
          │Sui2NapCat│   │  ┌─────────┐ │
          │  (QQ)    │◄──┤  │ 引擎    │ │
          └──────────┘   │  │ ┌──────┐│ │
                         │  │ │记忆  ││ │
          ┌──────────┐   │  │ ├──────┤│ │
          │Sui2vtuber│   │  │ │情感  ││ │
          └──────────┘   │  │ ├──────┤│ │
                         │  │ │性格  ││ │
          ┌──────────┐   │  │ └──────┘│ │
          │ Sui2tg   │   │  └─────────┘ │
          └──────────┘   └──────────────┘
          ┌──────────┐
          │Sui2mine  │
          │ -craft   │
          └──────────┘
```

### 通信协议

所有 Hand ↔ Core 的通信统一通过 **WebSocket**，使用 JSON 消息格式：

```json
{
  "type": "input | output | status | command",
  "from": "hand_name",
  "to": "core | hand_name",
  "payload": { ... }
}
```

### 数据流

```
外部平台 → Hand → WS → SuiCore（技能处理）→ WS → Hand → 外部平台
```

---

## 📜 许可证

Copyright (c) 2026 Sui-With-u

本组织下所有仓库均使用 **PolyForm Noncommercial License 1.0.0** 许可。
仅允许**非商业用途**。

详见 [LICENSE](https://github.com/sui-with-u/.github/blob/main/LICENSE) 文件。

---

</details>

<details>
<summary><b>🇬🇧 English</b></summary>

<br>

## 🌾 Sui Ecosystem

**SuiBot** is a modular AI character ecosystem. Its name comes from the Chinese character **「穗」** (suì), symbolizing harvest and hope.

It consists of two layers:

| Layer | Description |
|-------|-------------|
| **Core** | The brain. Built-in Skills (LLM / TTS / OCR / STT) + Emotion / Memory / Personality engines |
| **Hands** | Independent repositories, each connecting to an external platform via WebSocket |

> One SuiCore + many paws = SuiBot ecosystem

---

## 📦 Repositories

| Repository | Description | Status |
|------------|-------------|--------|
| [SuiBot](https://github.com/sui-with-u/SuiBot) | Main repo, ecosystem overview & docs | 🚧 Building |
| [SuiCore](https://github.com/sui-with-u/SuiCore) | Core brain, built-in Skills, WS server | 🚧 Building |
| [SuiWeb](https://github.com/sui-with-u/SuiWeb) | Web dashboard, visualization & management | 🚧 Building |
| [Sui2NapCatQQ](https://github.com/sui-with-u/Sui2NapCatQQ) | QQ bidirectional messaging (via NapCat) | 📌 Planned |
| [Sui2vtuber](https://github.com/sui-with-u/Sui2vtuber) | VTubeStudio model control | 📌 Planned |
| [Sui2tg](https://github.com/sui-with-u/Sui2tg) | Telegram bot | 📌 Planned |
| [Sui2minecraft](https://github.com/sui-with-u/Sui2minecraft) | Minecraft chat / commands / automation | 📌 Planned |

---

## 🏗 Architecture

```
                         ┌──────────────┐
                         │   SuiCore    │
                         │  ┌─────────┐ │
               ┌─────────┤  │ Skills  │ │
               │         │  │ ┌─────┐ │ │
               │         │  │ │ LLM │ │ │
               │         │  │ ├─────┤ │ │
               │         │  │ │ TTS │ │ │
               │ WS      │  │ ├─────┤ │ │
          ┌────┴─────┐   │  │ │ OCR │ │ │
          │  SuiWeb  │   │  │ ├─────┤ │ │
          └──────────┘   │  │ │ STT │ │ │
                         │  │ └─────┘ │ │
          ┌──────────┐   │  └─────────┘ │
          │Sui2NapCat│   │  ┌─────────┐ │
          │  (QQ)    │◄──┤  │ Engine  │ │
          └──────────┘   │  │ ┌──────┐│ │
                         │  │ │Memory││ │
          ┌──────────┐   │  │ ├──────┤│ │
          │Sui2vtuber│   │  │ │Emotion││ │
          └──────────┘   │  │ ├──────┤│ │
                         │  │ │Persona││ │
          ┌──────────┐   │  │ └──────┘│ │
          │ Sui2tg   │   │  └─────────┘ │
          └──────────┘   └──────────────┘
          ┌──────────┐
          │Sui2mine  │
          │ -craft   │
          └──────────┘
```

### Communication Protocol

All Hand ↔ Core communication uses **WebSocket** with JSON messages:

```json
{
  "type": "input | output | status | command",
  "from": "hand_name",
  "to": "core | hand_name",
  "payload": { ... }
}
```

### Data Flow

```
External Platform → Hand → WS → SuiCore (Skills processing) → WS → Hand → External Platform
```

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
