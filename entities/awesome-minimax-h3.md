---
title: awesome-minimax-h3
created: 2026-08-14
updated: 2026-08-14
type: entity
tags: [open-source, multimodal, tool, prompt-engineering]
sources: [https://github.com/ZeroLu/awesome-minimax-h3]
---

# Awesome MiniMax H3

社区精选的 MiniMax H3 视频生成提示词合集，收录来自 X (Twitter) 和顶级提示词工程师的高保真视频生成 prompt。涵盖教育纪录片、动作电影、情景喜剧、音乐同步展示等 6 大类别。

- GitHub: [github.com/ZeroLu/awesome-minimax-h3](https://github.com/ZeroLu/awesome-minimax-h3)
- Stars: 1+（早期阶段，2026-08-12 创建）
- 语言: Shell（README 编排）
- 创建: 2026-08-12
- 许可: MIT
- 多语言: English / 简体中文
- 作者: ZeroLu（同一作者还维护 [[awesome-seedance]] 和 [[awesome-gpt-image]]）

## 内容分类

| 类别 | 示例风格 |
|------|----------|
| 教育与讲解 | ABC 学习动画、字母拼读、儿童益智 |
| 纪录片与 Vlog 写实 | 真实纪录片质感、Vlog 视角 |
| 电影动作 | 动作场面、动作电影、追击 |
| 情景喜剧与角色对话 | 情景喜剧片段、角色对话 |
| 音乐同步展示 | 音乐卡点、节奏同步视频 |
| 社区展示 | 社区创作的精选案例 |

## 提示词结构模式

所有提示词遵循统一的 **时间戳+阶段描述** 结构：

```
[00:00-00:01] Introduction
  角色/场景描述 → 动作 → 镜头切换

[00:01-00:04] A is for Apple
  大写字母 → 音效 → 物体 → 俏皮动作 → 物体名

[+ Style]          视觉风格声明（圆角 3D / 柔和粉彩 / 工作室灯光）
[+ Visual style]   高级极简技术美学（白色空间、优雅构图、微妙反射）
```

## 精选提示词示例：ABC 学习动画

```
Create a 15-second animated educational video that teaches young children
the letters A, B, C, and D.

The learning pattern for every letter must be:
LETTER → SOUND → OBJECT → PLAYFUL ACTION → OBJECT NAME

Target audience: children ages 3 to 6.

Visual style:
Use adorable rounded 3D characters, soft pastel colors, gentle facial
expressions, and simple recognizable objects. Combine this with a
premium minimalist technology aesthetic featuring clean white space,
elegant composition, soft studio lighting, subtle reflections, smooth
gradients, rounded geometry, crisp typography, and extremely polished
transitions.

Use a clean off-white background with a different soft color glow
behind each letter.

0:00–0:01 | Introduction
A small smiling star mascot bounces into the center of the screen.
The mascot taps the screen, creating a soft ripple that reveals the
first letter.

0:01–0:04 | A is for Apple
Show a large uppercase "A" and smaller lowercase "a" beside it.
The narrator says: "A. A says ah. A is for Apple."
The uppercase A gently inflates and transforms into a shiny red apple.
```

## 关键技术要点

- **统一学习模式**（以教育类为例）：LETTER → SOUND → OBJECT → PLAYFUL ACTION → OBJECT NAME
- **风格声明前置**：开头明确视觉风格（圆角 3D / 柔和粉彩 / 工作室灯光等）
- **时间戳细分**：每 1-4 秒一个明确阶段
- **极简美学**：clean white space、elegant composition、subtle reflections
- **多感官设计**：视觉 + 音效 + 旁白 + 文字同步
- **圆滑几何**：rounded geometry、crisp typography、polished transitions

## 与 [[awesome-seedance]] 的关系

两个仓库来自同一作者 ZeroLu，是 **MiniMax H3 与 Seedance 2.0 提示词社区的双子星**：

| 维度 | awesome-seedance | awesome-minimax-h3 |
|------|------------------|---------------------|
| 模型 | Seedance 2.0（字节即梦） | MiniMax H3（MiniMax 视频生成） |
| 时间 | 2026-02 创建（1.7k stars） | 2026-08 创建（早期） |
| 类别 | 7 大类（电影/广告/社交/动漫等） | 6 大类（教育/纪录片/动作/喜剧等） |
| 风格 | 时间戳 Shot 结构 + 电影摄影术语 | 时间戳阶段描述 + 教学场景模板 |

共同特点：**都从 X/Twitter 社区精选、都保留原始提示词、都按风格分类、都支持多语言 README**。

## 与 [[seedance-product-video]] 的关系

- awesome-minimax-h3 提供灵感库（社区精选提示词）
- seedance-product-video 提供自动化生成工作流（Agent Skill）
- 两者互补：先在 awesome-* 找灵感，再用 Skill 自动化生成

## 相关页面

- [[awesome-seedance]] — 同作者的 Seedance 2.0 提示词库（1.7k stars）
- [[awesome-gpt-image]] — 同作者的 GPT Image 2 提示词库（1.2k stars）
- [[seedance-product-video]] — Seedance 自动化产品视频提示词 Skill
- [[ai-image-generation]] — AI 图像/视频生成技术生态
- [[baoyu-skills]] — 内容生成 Agent 技能集合