---
title: video-use
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, agent, tool, ai]
sources: [https://mp.weixin.qq.com/s/rmS4IFn9Ec_xmiEs7RGBSg, https://github.com/browser-use/video-use]
---

# Video Use

## Overview

来自 Browser Use 团队的开源视频剪辑技能，让 Claude Code 通过自然语言指令自动完成视频剪辑。团队此前开源的 browser-use（AI 自动操控浏览器）已获 8.8 万 Star，Video Use 是同一套方法论在视频编辑领域的复用。

- GitHub: [github.com/browser-use/video-use](https://github.com/browser-use/video-use)
- Stars: 7,051+
- 语言: Python
- 创建: 2026-04-12
- 定位: Claude Code 视频剪辑技能（Skill）
- 描述: Edit videos with coding agents

## 核心能力

| 能力 | 说明 |
|------|------|
| 自然语言驱动 | 用一句话描述需求，AI 自动完成全部剪辑 |
| 口头禅清理 | 自动识别并剪掉"呃"、"嗯"等多余语气片段 |
| 色彩调级 | 对每段素材做色彩调级 |
| 音频淡入淡出 | 每个剪切点自动加 30ms 音频渐变 |
| 字幕生成 | 自动生成字幕 |
| 自动合并 | 输出剪辑合并完成的最终视频 |
| 项目记忆 | 剪辑上下文写入 project.md，支持断点续剪 |

## 技术实现：两层架构

### 第一层：音频层（常驻加载）

- 通过 **ElevenLabs Scribe** 转写音频
- 生成**带词级时间戳**的文字稿（剪辑精度的关键）
- 同时标注说话人、笑声、叹息等信息
- Scribe 是少数同时提供词级时间戳 + 说话人区分的转写工具

### 第二层：视觉层（按需调用）

- `timeline_view` 在关键决策时现场合成图片给 LLM
- 图片包含：胶片缩略图 + 音频波形 + 单词标签叠加
- 类似 browser-use 用结构化 DOM 替代网页截图的思路

### 自检机制

每次渲染后自动扫描检查：
- 画面跳切
- 爆音
- 字幕遮挡

有问题自动回炉重新渲染，最多 3 次，通过后才交付预览。

## 工作流程

```
转录 → 打包 → 模型推理 → 生成剪辑决策 → 渲染 → 自检
```

每一步都需要用户确认才执行，不会自动"下刀"。

## 使用示例

```
> 把 xxx 文件夹里的视频素材剪辑成一条可发布的视频
```

AI 会自动：
1. 盘点素材
2. 给出剪辑方案
3. 等待确认
4. 自动识别并剪掉口头禅片段
5. 色彩调级 + 音频淡入淡出
6. 添加字幕
7. 输出最终视频到素材目录旁边的文件夹

## 安装

```bash
# 克隆项目
git clone https://github.com/browser-use/video-use.git
cd video-use

# 链接到 Claude Code skills 目录
ln -s $(pwd) ~/.claude/skills/video-use

# 安装依赖
brew install ffmpeg      # 必装
brew install yt-dlp      # 可选，用于下载在线素材

# 配置 ElevenLabs API Key
cp .env.example .env
# 编辑 .env 填入 ELEVENLABS_API_KEY
```

## 前置依赖

| 依赖 | 说明 |
|------|------|
| Claude Code | AI 编程 Agent |
| ffmpeg | 视频处理（必装） |
| ElevenLabs API Key | 语音转录（必装） |
| yt-dlp | 在线素材下载（可选） |

## 方法论复用

作者在两个项目中验证了同一套方法论：

| 项目 | 传统方式 | 创新方式 |
|------|---------|---------|
| browser-use | 给 LLM 喂网页截图 | 喂结构化 DOM |
| Video Use | 给 LLM 喂视频帧 | 喂带时间戳的转录文本 |

核心思路：**用结构化中间表示替代原始数据**，大幅降低 token 消耗，提升理解精度。

## 当前状态

- 早期阶段，复杂场景可能需要多轮对话
- 描述越具体，结果越准确
- 支持断点续剪（同一项目的剪辑上下文持久化）

## 生态关系

- 属于 [[claude-code-skills]] 生态中的视频编辑技能
- 团队前作 browser-use（8.8 万 Star）验证了 AI 操控浏览器的方法论
- 与 [[baoyu-skills]] 中的内容生成技能互补——baoyu 偏图文，video-use 偏视频
