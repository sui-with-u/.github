<p align="center">
  <img src="https://raw.githubusercontent.com/sui-with-u/.github/main/profile/banner.svg" alt="Sui-With-u" width="600">
</p>

<h3 align="center">“夜来南风起，小麦覆陇黄”</h3>

<h3 align="center">「穗」，象征着丰收与希望，麦穗黄、九穗嘉禾。</h3>

<p align="center">
  <a href="#-suit-生态">生态</a> ·
  <a href="#-repositories">仓库</a> ·
  <a href="#-architecture">架构</a> ·
  <a href="#-license">许可证</a>
</p>

![](https://img.shields.io/badge/status-building-7C3AED?style=flat-square)
![](https://img.shields.io/badge/license-PolyForm%20Noncommercial-3B82F6?style=flat-square)

---

## 🌾 Sui 生态

**SuiBot** 是一个模块化的 AI 角色生态。名称取自汉字 **「穗」**（suì），象征丰收与希望。

它由两个层次构成：

| 层 | 说明 |
|----|------|
| **Core** | 大脑。内置 Skills（LLM / TTS / OCR / STT）+ 情感 / 记忆 / 性格引擎 |
| **Hands** | 触手。独立仓库，每个连接一个外部平台，通过 WebSocket 与 Core 通信 |

> 一个核心（SuiCore）+ 五只手 = SuiBot 生态

---

## 📦 Repositories

| 仓库 | 说明 | 状态 |
|------|------|------|
| [SuiCore](https://github.com/sui-with-u/SuiCore) | 核心大脑，内置 Skills，WS 服务端 | 🚧 开发中 |
| [SuiWeb](https://github.com/sui-with-u/SuiWeb) | Web 管理面板，可视化 + 数据管理 | 🚧 开发中 |
| [Sui2NapCatQQ](https://github.com/sui-with-u/Sui2NapCatQQ) | QQ 双向消息（NapCat 中间件） | 📌 待开发 |
| [Sui2vtuber](https://github.com/sui-with-u/Sui2vtuber) | VTubeStudio 皮套控制 | 📌 待开发 |
| [Sui2tg](https://github.com/sui-with-u/Sui2tg) | Telegram 机器人 | 📌 待开发 |
| [Sui2minecraft](https://github.com/sui-with-u/Sui2minecraft) | Minecraft 聊天 / 指令 / 自动化 | 📌 待开发 |

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
外部平台 → Hand → WS → SuiCore（Skills 处理）→ WS → Hand → 外部平台
```

---

## 📜 License

Copyright (c) 2026 Sui-With-u

All repositories in this organization are licensed under the **PolyForm Noncommercial License 1.0.0**.  
You may use, modify, and distribute the software for **noncommercial purposes only**.

See the [LICENSE](https://github.com/sui-with-u/.github/blob/main/LICENSE) file for details.

---

<p align="center">
  <sub>穗穗碎碎念 · Sui-With-u</sub>
</p>
