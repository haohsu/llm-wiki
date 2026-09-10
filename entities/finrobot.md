---
title: FinRobot
created: 2026-09-10
updated: 2026-09-10
type: entity
tags: [agent, model, tool, open-source]
sources: [raw/articles/awesome-llm-trading-agents.md, https://github.com/AI4Finance-Foundation/FinRobot]
---

# FinRobot

- **GitHub**: https://github.com/AI4Finance-Foundation/FinRobot
- **Stars**: 7,955（2026-09 快照）
- **活跃度**: 2026-09-07 有 push
- **组织**: AI4Finance Foundation（FinRL / FinGPT 同门）

## 是什么

AI4Finance 基金会的**开源金融 AI Agent 平台**，学术风格的股票研究、市场预测、研报生成。与 FinGPT（金融 LLM 微调栈）是上层 platform / 下层 model 的关系。

- 组合 LLM + 强化学习 + 量化分析
- 覆盖 forecasting / document-analysis / trading-strategy 三类 agent
- 全程 financial chain-of-thought prompt
- arXiv 2405.14767（2024）论文支撑

## 诚实评估（来自 awesome-llm-trading-agents）

- 平台式广度大，但**未必每个模块都是完整实现**——评估 trading-strategy agent 时要确认是否有端到端 backtest 示例
- 与 FinGPT 的关系容易被误读：FinGPT 是微调 LM，不是独立交易系统，FinRobot 才是 agent 平台

## 与生态的关系

- 是 [[llm-trading-ecosystem]] 中"近亲（不同技术路线）"一节的代表：LLM Agent 平台路线 vs TradingAgents 的辩论框架路线
- 上游 [[fingpt]]（金融 LLM LoRA 微调栈）见 [[llm-trading-ecosystem]]
- 与 FinRL（深度强化学习路线，16.2k stars）并列 AI4Finance 三条产品线

## 相关页面

- [[llm-trading-ecosystem]] — 生态总览
- [[trading-agents]] — 辩论制对照
- [[ai-hedge-fund]] — 另一种非学术路线