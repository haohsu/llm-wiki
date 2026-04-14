---
title: Harness Engineering vs Context Engineering 概念辨析
created: 2026-04-14
updated: 2026-04-14
type: comparison
tags: [agent, architecture, comparison]
sources: [raw/articles/Beyond Prompts and Context Harness Engineering for AI Agents.md, raw/articles/Harness Engineering The Complete Guide to Building Systems That Make AI Agents Actually Work (2026).md, raw/articles/Effective context engineering for AI agents.md]
---

# Harness Engineering vs Context Engineering 概念辨析

## 三层嵌套关系

这三个概念可以理解为嵌套层，从 Prompt → Context → Harness 不断扩展：

**Harness Engineering ⊃ Context Engineering ⊃ Prompt Engineering**

## 详细对比

| 概念 | 核心问题 | 设计目标 | 典型场景 |
| --- | --- | --- | --- |
| **Prompt Engineering** | "怎么措辞？" | 发送给 LLM 的指令文本 | 单次交互优化、角色设定、few-shot 示例 |
| **Context Engineering** | "模型看到什么？" | 推理时 LLM 看到的所有 token | RAG、MCP、记忆管理、上下文窗口优化 |
| **Harness Engineering** | "系统阻止、度量和修复什么？" | Agent 外部的约束、反馈和操作系统 | 架构约束、确定性验证、熵治理、安全护栏、生命周期管理 |

## Prompt Engineering

关注单次交互中的指令质量。

核心方法：
- 角色设定和系统提示
- 思维链（Chain-of-Thought）
- Few-shot 示例
- 输出格式控制

**局限**：解决"问得好"的问题，但不解决"Agent 运行环境"的问题。

## Context Engineering

Anthropic 的定义：**在 LLM 推理过程中策划和维护最优 token 集合的策略集合**。

核心关注：
- **Context Rot**：上下文窗口填满时模型性能下降
- **注意力预算**：每个 token 消耗一定的注意力资源
- **渐进式披露**：Agent 只在需要时获取特定信息
- **Compaction**：上下文窗口接近满时的智能压缩

三大长时任务策略：
1. **Compaction**：对话历史压缩后重启新上下文窗口
2. **结构化笔记**：Agent 定期将笔记持久化到外部存储
3. **子 Agent 架构**：专用子 Agent 处理聚焦任务，保持干净上下文

**局限**：解决"模型看到什么"的问题，但不覆盖架构约束、机械验证、安全护栏等"模型看不到"的系统层面。

## Harness Engineering

在此基础上额外覆盖：

| 维度 | Context Engineering | Harness Engineering 增加 |
| --- | --- | --- |
| 信息流 | 管理模型看到什么 | 管理系统阻止/度量/修复什么 |
| 执行层 | 优化推理时 token | 机械执行（Linter、CI、结构测试） |
| 安全 | 提示级安全指令 | 基础设施级安全护栏（最小权限、出口控制、审计日志） |
| 生命周期 | 上下文窗口管理 | 跨会话状态持久化、Agent 生死管理 |
| 质量保证 | 提供好的上下文 | 确定性验证 + 熵治理 |

## 类比理解

如果 Prompt Engineering 是命令"右转"，那么：
- **Context Engineering** 是帮助马理解方向的一切：地图、路标、可见地形
- **Harness Engineering** 是更大的设计：缰绳、马鞍、围栏、道路本身——让十匹马能同时安全奔跑

## 两种视角

1. **包含视角**（直观）：Harness > Context > Prompt
2. **功能视角**（实用）：Context Engineering 帮模型思考，Harness Engineering 防止整个系统偏离轨道

实践中有用的不是框架本身，而是认识到**存在上下文设计无法单独解决的问题**。

## 实际关系

Harness Engineering 将 Context Engineering 作为子集，同时包含：
- 架构约束（确定性 Linter + LLM Agent 双重监控）
- 确定性验证（CI、测试）
- 熵治理（后台 Agent 定期清理）
- 安全护栏（最小权限、出口控制）
- 生命周期管理（Agent 启动、持久化、恢复）

## 相关页面
- [[harness-engineering]] — 核心概念
- [[harness-engineering-components]] — Harness 四大支柱
- [[agent-harness-patterns]] — 实践模式
