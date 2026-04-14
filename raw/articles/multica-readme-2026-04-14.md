---
title: "Multica — Open-Source Managed Agents Platform"
source: "https://github.com/multica-ai/multica"
author:
  - "[[multica-ai]]"
published: 2026-04-14
created: 2026-04-14
description: "Multica 是开源的 managed agents 平台，将 AI 编码 Agent 变成真正的团队成员。支持 Claude Code、Codex、OpenClaw、OpenCode。Go 后端 + Next.js 前端 + PostgreSQL。"
tags:
  - "clippings"
---

# Multica — Your Next 10 Hires Won't Be Human

Stars: 11,558 | Forks: 1,430 | Created: 2026-01-13 | TypeScript

## 概述

Multica 是一个开源的 managed agents 平台。你可以像给真人分配 GitHub Issue 一样给 AI Agent 分配任务——Agent 自主领取工作、写代码、报告阻塞、更新状态。

## 核心特性

- **Agent as Teammates**：Agent 有个人资料，出现在看板上，发评论、建 Issue、主动报告阻塞
- **自主执行**：完整任务生命周期（排队→认领→开始→完成/失败），WebSocket 实时进度流
- **可复用 Skills**：每次解决方案变成团队的可复用 Skill，部署/迁移/代码审查随时间复利
- **统一运行时**：一个 Dashboard 管理所有计算——本地守护进程和云端运行时，自动检测可用 CLI
- **多工作空间**：按团队组织工作，工作空间级别隔离（各自 Agent、Issue、设置）

## 支持的 Agent Provider

Claude Code (Anthropic)、Codex (OpenAI)、OpenClaw、OpenCode

## 技术栈

| 层 | 技术 |
| --- | --- |
| 前端 | Next.js 16 (App Router), TypeScript, CSS |
| 后端 | Go (Chi router, sqlc, gorilla/websocket) |
| 数据库 | PostgreSQL 17 + pgvector |
| Agent 运行时 | 本地守护进程执行 Claude/Codex/OpenClaw/OpenCode |

## 安装

- macOS/Linux: `brew install multica-ai/tap/multica`
- Windows: `irm https://raw.githubusercontent.com/multica-ai/multica/main/scripts/install.ps1 | iex`
- 自托管: Docker-based, `--with-server` flag

## 架构

```
Next.js Frontend → Go Backend (Chi + WebSocket) → PostgreSQL 17 (pgvector)
                          |
                 Agent Daemon (本地运行)
                 Claude / Codex / OpenClaw / OpenCode
```

## Top 贡献者

| 贡献者 | Commits |
| --- | --- |
| forrestchang | 710 |
| NevilleQingNY | 680 |
| Bohan-J | 431 |
| ldnvnbl | 371 |
