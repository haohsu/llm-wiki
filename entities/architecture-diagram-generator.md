---
title: architecture-diagram-generator
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, agent, tool, product]
sources: [https://github.com/Cocoon-AI/architecture-diagram-generator]
---

# Architecture Diagram Generator

Claude Skill，用自然语言描述系统架构后秒级生成暗色主题专业架构图，输出为独立 HTML 文件，支持导出 PNG/PDF。

- GitHub: [github.com/Cocoon-AI/architecture-diagram-generator](https://github.com/Cocoon-AI/architecture-diagram-generator)
- Stars: 4,833 | Forks: 362
- 语言: HTML
- 创建: 2025-12-22
- 许可: MIT
- 作者: Cocoon-AI

## 核心功能

> Need an architecture diagram? Get AI to build you one.

- **无需设计技能** — 用自然语言描述架构即可
- **快速迭代** — 通过对话添加组件、修改布局、更新样式
- **独立输出** — 单个 HTML 文件，内嵌 CSS + 内联 SVG
- **导出内置** — 复制 PNG / 下载 PNG / 下载 PDF 按钮

## 三步使用

### 1. 安装 Skill

下载 `architecture-diagram.zip` → claude.ai → Customize → Skills → Upload a skill

或 Claude Code CLI：
```bash
unzip architecture-diagram.zip -d ~/.claude/skills/
```

### 2. 获取架构描述

三种方式：
- **AI 分析代码库** — 用 Cursor/Claude Code/Windsurf 分析代码生成描述
- **自己写** — 列出组件和连接关系
- **问 Claude** — 「SaaS 应用的典型架构是什么？」

### 3. 生成图表

```
Use your architecture diagram skill to create an architecture diagram from this description:

- React frontend talking to a Node.js API
- PostgreSQL database
- Redis for caching
- Hosted on AWS with CloudFront CDN
```

## 语义色彩系统

| 组件类型 | 颜色 | 用途 |
|----------|------|------|
| Frontend | Cyan（青） | 客户端应用、UI、边缘设备 |
| Backend | Emerald（绿） | 服务器、API、服务 |
| Database | Violet（紫） | 数据库、存储、AI/ML |
| Cloud/AWS | Amber（琥珀） | 云服务、基础设施 |
| Security | Rose（玫红） | 认证、安全组、加密 |
| External | Slate（灰） | 通用、外部系统 |

## 设计特点

- **暗色主题** — Slate-950 背景 + 微妙网格图案
- **专业排版** — JetBrains Mono 字体
- **智能分层** — 箭头在组件框后方干净渲染
- **浏览器直接打开** — 无需安装任何软件

## 导出方式

| 方式 | 说明 |
|------|------|
| 📋 Copy | 高分辨率 PNG 复制到剪贴板，可粘贴到 Slides/Docs/Slack |
| 🖼️ PNG | 下载高分辨率 PNG 文件 |
| 📄 PDF | 下载保留暗色主题的 PDF |

## 常见场景示例

**Web 应用：** React + Node.js/Express API + PostgreSQL + Redis + JWT

**AWS Serverless：** CloudFront + API Gateway + Lambda + DynamoDB + S3 + Cognito

**微服务：** React + Kong API Gateway + 多语言服务（Go/Java/Python）+ 多数据库 + Kafka + Kubernetes

## 与 [[excalidraw-diagram-generator]] 的对比

| 维度 | architecture-diagram-generator | [[excalidraw-diagram-generator]] |
|------|------|------|
| 定位 | 系统架构图（暗色主题） | 通用图表（手绘风格） |
| 风格 | 专业暗色 + 语义色彩 | Excalidraw 手绘 |
| 图表类型 | 架构图专精 | 9 种（流程图/架构图/ER图等） |
| 输出格式 | 独立 HTML（内嵌 SVG） | .excalidraw JSON |
| 安装方式 | Claude Skill（claude.ai / CLI） | Claude Code Skill |
| 适合场景 | 系统架构展示、技术文档 | 通用图表、白板协作 |

## 适用场景

- 快速生成系统架构图（无需设计技能）
- 技术文档和演示文稿配图
- 团队架构讨论和评审
- 将代码库自动转为可视化架构图

## 局限性

- 仅支持架构图，不支持其他图表类型
- 暗色主题固定，无亮色模式
- 依赖 Claude Code Execution 功能
- 复杂架构可能需要多轮迭代

## 相关页面

- [[excalidraw-diagram-generator]] — 同类图表生成技能，支持更多图表类型
- [[baoyu-skills]] — baoyu-diagram 同类 SVG 图表生成
- [[claude-code-skills]] — 属于 Claude Code 技能生态
- [[knowledge-as-code]] — 架构图是知识可视化的重要形式
