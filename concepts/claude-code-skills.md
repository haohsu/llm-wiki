---
title: Claude Code Skills
created: 2026-04-12
updated: 2026-04-12
type: concept
tags: [agent, tool, platform, open-source]
sources: [raw/articles/baoyu-skills-readme-2026-04-12.md]
---

# Claude Code Skills

## Definition
Claude Code 的技能/插件系统，允许开发者扩展 Claude Code 的能力。技能是以目录形式组织的命令集，通过 Plugin Marketplace 或工具（如 ClawHub、npx）分发和安装。

## 核心概念
- **Skill**: 一个可执行的命令单元，通常包含 prompt 模板、工具脚本和配置
- **Plugin**: 多个 skill 的打包集合
- **Marketplace**: 技能分发渠道（Claude Code Plugin Marketplace、ClawHub 等）

## 安装模式
| 方式 | 命令 | 特点 |
|------|------|------|
| npx | `npx skills add author/repo` | 最简单，直接从 GitHub |
| Plugin Marketplace | `/plugin install name@marketplace` | Claude Code 原生集成 |
| ClawHub | `clawhub install skill-name` | 独立安装单个 skill |

## 典型技能类型（基于 [[baoyu-skills]] 分析）
1. **内容生成**: 信息图、图表、PPT、漫画、封面图
2. **AI 后端集成**: 图像生成（多 provider 抽象）
3. **发布工具**: 微博、微信、X 等平台自动化发布
4. **内容处理**: URL 提取、翻译、格式化、压缩

## 设计模式观察
- 技能倾向于 **维度组合** 而非固定选项（如 Style × Layout × Palette）
- 发布类技能需要 **浏览器自动化** 绕过反爬
- 图像生成技能趋向 **多 provider 统一接口**
- SVG 手写 > 图像模型生成（更可控、可编辑）

## 竞品/同类
- [[baoyu-skills]] — 当前最流行的 Claude Code 技能集合（14K+ stars）
- Hermes Agent Skills — 类似架构但更侧重 CLI agent 场景

## 相关页面
- [[baoyu-skills]] — 标杆实现
- [[jim-liu]] — 生态关键人物
