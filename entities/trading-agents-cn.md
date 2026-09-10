---
title: TradingAgents-CN
created: 2026-09-10
updated: 2026-09-10
type: entity
tags: [agent, model, tool, market, open-source]
sources: [raw/articles/awesome-trading-agents.md, https://github.com/hsliuping/TradingAgents-CN]
---

# TradingAgents-CN

- **GitHub**: https://github.com/hsliuping/TradingAgents-CN
- **Stars**: 31,700（2026-09 快照，此前致力未收录，为 **A 股衍生版中最热**）
- **活跃度**: 2026-07-24 最后 push
- **定位**: TradingAgents 中文增强版，专为 A 股（沪深）场景调优

## 是什么

TradingAgents 的**中文 A 股 fork**，与上游（[[trading-agents]]，TauricResearch 原版，英文/美股）正面对比：
- 数据源换为 **Tushare / AkShare**（A 股行情、财报、龙虎榜）
- 输出**中文研究报告**
- 纳入 **A 股监管语境**（涨停跌停、T+1、ST 处理、监管公告等）

## 在生态中的位置

- 两个 awesome list 都收录为 A 股代表 fork，LLMQuant 列表明确标注 `TradingAgents-CN / TradingAgents-AShare` 为 A 股主线
- 是**数据源补缺**：正好弥补 [[public-apis]] 中 A 股数据源空缺（public-apis 以国际市场为主）
- A 股生态还有 [[trading-agents-ashare]]（KylinMountain，15 Agent + UI + Docker 一键部署）、oficcejo/aiagents-stock（1.9k stars，龙虎榜跟踪 + miniqmt 实盘）、Miasyster/QuantGPT（agent 驱动 A 股因子工厂）

## 相关页面

- [[trading-agents]] — 上游锚点项目
- [[llm-trading-ecosystem]] — 生态总览（A 股数据源衔接一节）
- [[public-apis]] — 国际市场 API 目录（A 股空缺的对照）