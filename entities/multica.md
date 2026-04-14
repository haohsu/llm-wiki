---
title: Multica
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [company, open-source, agent, product, platform]
sources: [raw/articles/multica-readme-2026-04-14.md]
---

# Multica

## 概述

Multica 是一个开源的 **managed agents 平台**，将 AI 编码 Agent 变成真正的团队成员。你可以像给真人分配 GitHub Issue 一样给 Agent 分配任务——Agent 自主领取工作、写代码、报告阻塞、更新状态。

口号：**"Your next 10 hires won't be human."**

定位为厂商中立、可自托管的人类 + AI 团队基础设施。

## 关键数据

| 指标 | 数据 |
| --- | --- |
| GitHub Stars | 11,558 |
| Forks | 1,430 |
| 创建时间 | 2026-01-13 |
| 主要语言 | TypeScript (~1.58MB) + Go (~1.24MB) |
| License | 自定义 |
| 官网 | https://multica.ai |

## 核心特性

### Agent as Teammates
- Agent 有个人资料，出现在看板上
- 发评论、建 Issue、主动报告阻塞
- 不是"工具调用者"，而是"团队成员"

### 自主执行
- 完整任务生命周期：排队 → 认领 → 开始 → 完成/失败
- WebSocket 实时进度流
- 无需人工中间干预

### 可复用 Skills
- 每次解决方案变成团队的可复用 Skill
- 部署、迁移、代码审查随时间复利
- 知识在团队中积累而非散落

### 统一运行时
- 一个 Dashboard 管理所有计算：本地守护进程 + 云端运行时
- 自动检测可用 CLI
- 实时监控

### 多工作空间
- 按团队组织工作
- 工作空间级别隔离（各自 Agent、Issue、设置）

## 支持的 Agent Provider

| Provider | 来源 |
| --- | --- |
| Claude Code | Anthropic |
| Codex | OpenAI |
| OpenClaw | 开源 |
| OpenCode | 开源 |

## 技术栈

| 层 | 技术 |
| --- | --- |
| 前端 | Next.js 16 (App Router), TypeScript, CSS |
| 后端 | Go (Chi router, sqlc, gorilla/websocket) |
| 数据库 | PostgreSQL 17 + pgvector |
| Agent 运行时 | 本地守护进程 |

### 架构
```
Next.js Frontend → Go Backend (Chi + WebSocket) → PostgreSQL 17 (pgvector)
                          |
                 Agent Daemon (本地运行)
                 Claude / Codex / OpenClaw / OpenCode
```

## 安装方式

- **macOS/Linux**: `brew install multica-ai/tap/multica`
- **Windows**: PowerShell 安装脚本
- **自托管**: Docker-based, `--with-server` flag

## 生态位分析

Multica 在 AI 编码 Agent 管理赛道中占据独特位置：

- vs **Claude Code / Codex CLI**：Multica 不是 Agent 本身，而是管理多个 Agent 的平台层
- vs **Linear / Jira**：Multica 的 Issue 可以被 Agent 直接领取和执行，不只是项目管理
- vs **GitHub Copilot Workspace**：Multica 厂商中立，支持多 Provider
- vs **[[langchain-agent-harness|LangChain DeepAgents]]**：LangChain 是 Harness 库，Multica 是完整的管理平台

核心差异化：**将 Agent 作为一等团队成员纳入项目管理流程**，而非仅仅作为代码生成工具。

## Top 贡献者

| 贡献者 | Commits |
| --- | --- |
| forrestchang | 710 |
| NevilleQingNY | 680 |
| Bohan-J | 431 |
| ldnvnbl | 371 |

## 相关页面
- [[harness-engineering]] — Harness Engineering 是 Multica 的理论基础
- [[agent-harness-patterns]] — Agent Harness 实践模式
- [[claude-code-skills]] — Claude Code 技能生态（Multica 支持的 Provider 之一）
