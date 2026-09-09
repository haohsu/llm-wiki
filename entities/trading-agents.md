---
title: TradingAgents
created: 2026-05-01
updated: 2026-09-09
type: entity
tags: [agent, model, tool]
sources: [raw/articles/jike-github-trending-2026-05-01.md]
---

# TradingAgents

- **GitHub**: https://github.com/TauricResearch/TradingAgents
- **Stars**: 57,850
TradingAgents 是一个基于多智能体 LLM 的金融交易框架，模拟真实交易公司的运作，提供多种专业代理协作分析市场并指导交易决策。

## 核心特性

- 多 Agent 协作架构，模拟真实交易公司组织结构
- LLM 驱动的市场分析和交易决策
- 多种专业代理分工协作

## 与生态的关系

- 典型的 [[agent-harness-patterns]] 实践：多 Agent 并行 + 专业化分工
- 与 [[anthropic-agent-harness]] 中的多 Agent 研究系统理念相似
- 金融领域 Agent 应用的标杆项目

## 同类项目与生态

完整生态盘点见 [[llm-trading-ecosystem]]。要点：同类中最知名的是 virattt/ai-hedge-fund（~59k stars，投资人 persona 辩论）；A 股场景有 TradingAgents-CN（Tushare/AkShare 数据源）和 TradingAgents-AShare（15 Agent + UI）两个衍生版。已知局限：LLM 训练集泄漏、回测池小、新闻延迟 → 定位 swing/波段研究辅助，非自动盈利系统。
