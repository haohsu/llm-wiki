---
title: Seedance-Product-Video
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, agent, tool, product]
sources: [https://github.com/op7418/Seedance-Product-Video]
---

# Seedance-Product-Video — Seedance 产品宣传视频提示词技能

为 Seedance 2.0 视频生成模型撰写产品宣传动画提示词的 Claude Code Skill。生成 15 秒一镜到底 motion graphics 提示词，支持 4 种美学风格。

- GitHub: [github.com/op7418/Seedance-Product-Video](https://github.com/op7418/Seedance-Product-Video)
- Stars: 132 | Forks: 13
- 创建: 2026-04-13
- 许可: MIT
- 作者: op7418（提示词灵感来自 [@oggii_0](https://x.com/oggii_0)）

## 核心功能

一句话描述：**用 AI 为 Seedance 2.0 生成专业级产品宣传视频提示词。**

- 15 秒一镜到底（one-take, no cuts），5-6 个连续形变阶段
- 4 种美学风格可选
- 支持垫图（参考图）模式，自动标注图片占位符
- 生成后可通过即梦 Dreamina CLI 直接生成视频

## 四种美学风格

| 风格 | 氛围 | 最佳场景 |
|------|------|----------|
| A: Apple Cupertino | 磨砂玻璃、钛金属深度 | 旗舰产品、高端硬件 |
| B: Microsoft Fluent | 亚克力层叠、彩色渐变 | 生产力工具、平台 |
| C: Bauhaus / 原研哉 | 哑光禅意、极简留白 | 效率工具、阅读器 |
| D: Vercel / Linear | 虚空黑、霓虹线条 | 开发者工具、框架 |

## 提示词时间戳结构

```
0–2s   [STATE A → STATE B]    混沌凝结为第一形态
2–4s   [STATE B → STATE C]    融化/形变为第二形态
4–7s   [STATE C → STATE D]    包裹为复杂 3D 结构
7–10s  [STATE D → STATE E]    展平为动态 2D 图案
10–12s [STATE E → PRE-LOGO]   凝结为 logo 暗示
12–13s [HOLD]                  静默节拍
13–15s [LOGO]                  品牌揭示

+ Sound Design               音效弧线引用视觉时刻
+ Music                      背景音乐风格与节奏
+ Voiceover (inline)         嵌入时间轴阶段（如需要）
```

## 工作流程

1. 询问产品信息、需求、图片素材
2. 分析素材，选择最佳视觉风格
3. 生成 1000-2000 字符英文提示词（含时间戳结构）
4. 引导设置参考图（如有）
5. 可选：通过 Dreamina CLI 直接生成视频

## Dreamina CLI 集成

生成提示词后，技能自动检测 Dreamina CLI 是否已安装：

```bash
# 安装 Dreamina CLI
curl -fsSL https://jimeng.jianying.com/cli | bash

# 使用提示词生成视频
dreamina generate --prompt "..."
```

## 安装方式

```bash
# 推荐：npx skills
npx skills add op7418/Seedance-Product-Video -a claude-code

# 全局安装
npx skills add op7418/Seedance-Product-Video -a claude-code -g

# 手动安装
git clone https://github.com/op7418/Seedance-Product-Video.git ~/.claude/skills/seedance-prompt
```

## 文件结构

```
seedance-prompt/
├── SKILL.md                  # 主技能定义
├── README.md
└── references/
    └── prompt-system.md      # 提示词系统：美学矩阵 + 规则 + 模板
```

## 使用方式

```
/seedance-prompt
```

或自然语言：「帮我生成一个 Seedance 产品宣传视频的提示词」

## 与 [[ai-image-generation]] 的关系

Seedance 2.0 是字节跳动即梦（Dreamina）旗下的视频生成模型。本技能是 [[ai-image-generation]] 生态从**图片生成**向**视频生成**延伸的典型案例。

## 相关页面

- [[ai-image-generation]] — AI 图像/视频生成技术生态
- [[baoyu-skills]] — baoyu-imagine 集成即梦作为图像 provider
- [[ip-character-designer]] — 同类创意 Agent 技能，也使用即梦 CLI
- [[huashu-design]] — 另一种视觉内容生成工具
- [[video-use]] — 另一种视频相关 Agent 技能（剪辑方向）
