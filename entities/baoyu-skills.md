---
title: baoyu-skills
created: 2026-04-12
updated: 2026-04-12
type: entity
tags: [open-source, agent, tool, platform, api]
sources: [raw/articles/baoyu-skills-readme-2026-04-12.md]
---

# baoyu-skills

## Overview
由 [[jim-liu]]（宝玉）开发的 Claude Code 技能集合，旨在提升日常工作效率。14,192+ Stars，TypeScript 项目。支持 Claude Code Plugin Marketplace、ClawHub 和 npx 安装。

## Repository
- GitHub: [github.com/JimLiu/baoyu-skills](https://github.com/JimLiu/baoyu-skills)
- Stars: 14,192+
- 语言: TypeScript
- 创建: 2026-01-13
- Topics: agent-skills, claude-skills, codex-skills, openclaw-skills

## 三大类技能

### Content Skills（内容生成）
| 技能 | 功能 |
|------|------|
| `baoyu-xhs-images` | 小红书图片卡系列生成，12 种风格 × 6 种布局 |
| `baoyu-infographic` | 专业信息图生成，21 种布局 × 17 种视觉风格 |
| `baoyu-diagram` | SVG 图表生成（流程图、架构图、直觉图），Claude 手写 SVG |
| `baoyu-cover-image` | 文章封面图，5 维度系统（Type × Palette × Rendering × Text × Mood） |
| `baoyu-slide-deck` | PPT 幻灯片生成，自动合并为 .pptx/.pdf |
| `baoyu-comic` | 知识漫画，5 种画风 × 7 种语调 × 6 种布局 |
| `baoyu-article-illustrator` | 文章配图智能生成，分析结构自动选择插图类型 |
| `baoyu-post-to-x` | 发布到 X/Twitter（支持 X Articles） |
| `baoyu-post-to-wechat` | 发布到微信公众号（API + 浏览器两种模式） |
| `baoyu-post-to-weibo` | 发布到微博（支持头条文章） |

### AI Generation Skills（AI 生成后端）
| 技能 | 功能 |
|------|------|
| `baoyu-imagine` | AI 图像生成，集成 10+ provider（OpenAI、Google、DashScope、MiniMax、即梦、豆包等） |
| `baoyu-danger-gemini-web` | Gemini Web 交互（文本+图像生成） |

### Utility Skills（工具）
| 技能 | 功能 |
|------|------|
| `baoyu-youtube-transcript` | YouTube 字幕下载，支持多语言、翻译、章节、说话人识别 |
| `baoyu-url-to-markdown` | URL 转 Markdown |
| `baoyu-danger-x-to-markdown` | X/Twitter 内容转 Markdown |
| `baoyu-markdown-to-html` | Markdown 转 HTML |
| `baoyu-format-markdown` | Markdown 格式化 |
| `baoyu-translate` | 翻译工具 |
| `baoyu-compress-image` | 图片压缩 |
| `baoyu-image-cards` | 图片卡片生成 |
| `baoyu-image-gen` | 图片生成基础工具 |

## 安装方式
```bash
# 推荐
npx skills add jimliu/baoyu-skills

# Claude Code Plugin
/plugin marketplace add JimLiu/baoyu-skills
/plugin install baoyu-skills@baoyu-skills

# ClawHub
clawhub install baoyu-imagine
```

## 关键设计模式
- **多维度样式系统**: 几乎所有视觉技能都采用 维度组合 × 预设 的设计（如 Style × Layout × Palette）
- **多 Provider 自动选择**: `baoyu-imagine` 支持 10+ AI 图像 provider，自动检测可用 key 选择
- **SVG 手写**: `baoyu-diagram` 由 Claude 直接编写 SVG 代码而非调用图像模型
- **浏览器自动化**: 发布类技能使用 Chrome CDP 绕过反自动化检测

## 相关页面
- [[jim-liu]] — 项目作者
- [[claude-code-skills]] — Claude Code 技能生态背景
- [[ai-image-generation]] — AI 图像生成技术对比
