---
title: Anthropic Agent Harness 实践
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [company, agent, architecture]
sources: [raw/articles/Effective harnesses for long-running agents.md, raw/articles/Effective context engineering for AI agents.md, raw/articles/How we built our multi-agent research system.md, raw/articles/Building a C compiler with a team of parallel Claudes.md]
---

# Anthropic Agent Harness 实践

## 概述

Anthropic 是最早在官方工程博客中使用"Harness"一词描述 Agent 基础设施的公司之一（2025年11月）。其实践涵盖长时运行 Agent、上下文工程、多 Agent 研究系统和并行编译器构建，形成了完整的 Harness Engineering 知识体系。

## 长时运行 Agent 的 Harness

### 核心问题
Agent 在离散会话中工作，每个新会话无之前记忆。类似轮班工程师交接。

### 双 Agent 解决方案
1. **初始化 Agent**：首次运行搭建环境——特性列表、git 仓库、进度文件
2. **编码 Agent**：后续会话渐进推进，留下结构化更新

### 关键机制

**claude-progress.txt**
- 跨会话进度日志
- 新上下文窗口的 Agent 通过此文件 + git 历史快速理解工作状态

**特性列表（JSON）**
- 200+ 细粒度特性，每个带测试步骤
- 初始全部标记为 failing
- Agent 只能改 passes 字段
- 用 JSON（Agent 更不容易不当修改结构化数据）

**端到端测试**
- 提供 Puppeteer MCP 浏览器自动化
- Agent 倾向于不做端到端测试就标记完成——明确 prompt 要求必须用浏览器验证
- 截图记录验证过程

### 四大失败模式及对策

| 问题 | 初始化 Agent 对策 | 编码 Agent 对策 |
| --- | --- | --- |
| 过早宣布完成 | 创建特性列表文件 | 读特性列表，选择单一特性 |
| 遗留 bug 或未记录进度 | 初始化 git 和进度文件 | 读进度+git日志，运行基本测试 |
| 过早标记特性完成 | 设置特性列表 | 自验证后才标记 passing |
| 花时间搞清楚如何运行应用 | 写 init.sh 脚本 | 会话开始先读 init.sh |

## 上下文工程方法论

### 核心原则
- 找到**最小**的高信号 token 集合，最大化期望结果的概率
- 上下文是有限资源，边际收益递减
- Context Rot：token 增多时模型回忆准确度下降

### 系统提示的"正确高度"
在两种失败模式间的 Goldilocks 区间：
- 过度：复杂、脆弱的硬编码逻辑
- 不足：模糊、高层次指导，假设共享上下文

### 工具设计原则
- 自包含、错误健壮、用途明确
- 最小可行工具集——臃肿的工具集是常见失败模式
- 如果人类工程师都无法明确该用哪个工具，AI Agent 不可能做得更好

### 长时任务三大策略
1. **Compaction**：上下文窗口接近满时，总结内容并重启新窗口
2. **结构化笔记**：Agent 定期写笔记持久化到外部存储（Claude 玩 Pokemon 案例）
3. **子 Agent 架构**：专用子 Agent 处理聚焦任务，返回压缩摘要

## 多 Agent 研究系统

### 架构
- **编排者-工作者模式**：Lead Agent 协调，Subagent 并行搜索
- Lead Agent 分析查询 → 制定策略 → 生成 Subagent → 汇总结果 → CitationAgent 处理引用

### 实证数据
- 多 Agent 系统比单 Agent Opus 4 在内部研究评估上高出 90.2%
- Agent 通常消耗约 4x 更多 token（vs 聊天），多 Agent 系统约 15x
- token 使用量解释 80% 的性能方差

### 八大 Prompt 原则
1. 像 Agent 一样思考——构建模拟环境观察行为
2. 教编排者如何委派——详细任务描述避免重复工作
3. 按查询复杂度调整努力——简单查询 1 Agent，复杂研究 10+ Subagent
4. 工具设计至关重要——明确启发式规则
5. 让 Agent 改进自己——Claude 4 可以做优秀的 Prompt 工程师
6. 先广后窄——先探索全景再聚焦
7. 引导思考过程——扩展思考模式作为可控草稿纸
8. 并行工具调用——Lead Agent 并行生成 3-5 个 Subagent

## 并行编译器构建（Agent Teams）

### 实验数据
- 16 个并行 Claude Agent
- ~2000 次 Claude Code 会话
- $20,000 API 成本
- 10 万行 Rust C 编译器
- 可编译 Linux 6.9 内核（x86、ARM、RISC-V）

### 关键设计
- 每个 Agent 在独立 Docker 容器中
- 通过裸 git 仓库同步
- 任务锁机制（写入文本文件）
- Ralph Loop：完成后立即拾取下一个任务

### 关键发现
- 更强的模型（Opus 4.6 vs 4.5）需要重新设计 Harness
- Agent 无法感知时间流逝（时间盲）
- 测试验证器质量直接决定 Agent 产出质量

## 相关页面
- [[harness-engineering]] — 核心概念
- [[agent-harness-patterns]] — 实践模式
- [[openai-harness-engineering]] — OpenAI 实践对比
- [[langchain-agent-harness]] — LangChain 实践
