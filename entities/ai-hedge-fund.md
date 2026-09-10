---
title: ai-hedge-fund
created: 2026-09-10
updated: 2026-09-10
type: entity
tags: [agent, model, tool, market]
sources: [raw/articles/awesome-trading-agents.md, raw/articles/awesome-llm-trading-agents.md]
---

# ai-hedge-fund

- **GitHub**: https://github.com/virattt/ai-hedge-fund
- **Stars**: 63,323（2026-09 快照，从 ~59k 增长）
- **活跃度**: 2026-09-03 仍有 push

## 是什么

LLM 驱动的美股交易框架，repo 名即"AI 对冲基金"。核心是**投资人 persona 联合决策**：多位传奇投资人（Buffett / Munger / Burry / Cathie Wood 等，共 14 位 persona）各自提出观点，最后由 portfolio manager 拍板。与 TradingAgents 的全员辩论制不同，ai-hedge-fund 是 persona 集成 + 单层决策。

## 核心特性

- 14 位传奇投资人 persona 并行分析（价值、成长、逆向等流派全覆盖）
- 分析师 → 投资组合经理的层级决策
- 被大量 fork：51bitquant/ai-hedge-fund-crypto 等 crypto 变体（多时间框架 + 策略集成）

## 与生态的关系

- 与 [[trading-agents]] 并列为 LLM 交易 Agent 两大锚点项目（TradingAgents 更偏学术论文路线，ai-hedge-fund 更偏工程/社区 fork 路线）
- 分层生态中属于 **Multi-agent trading systems / Single-agent end-to-end traders** 层，完整盘点见 [[llm-trading-ecosystem]]
- 局限同 LLM 交易 agent 通病：训练集泄漏、回测偏差、新闻延迟 3-20 分钟（见 [[llm-trading-ecosystem]] 已知局限）

## 相关页面

- [[llm-trading-ecosystem]] — 生态总览
- [[trading-agents]] — 同期锚点项目（辩论制）
- [[trading-agents-cn]] — A 股中文衍生 fork（数据源路线不同）