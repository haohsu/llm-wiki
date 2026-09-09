---
title: LLM 交易 Agent 生态
created: 2026-09-09
updated: 2026-09-09
type: concept
tags: [agent, market, trend, comparison]
sources: [https://github.com/LLMQuant/awesome-trading-agents, https://github.com/bettyguo/awesome-llm-trading-agents]
---

# LLM 交易 Agent 生态

## Overview
以 [[trading-agents]]（2024，LangGraph 多 Agent 辩论架构）为锚点项目的开源生态盘点。数据来自 2026-05 的两个 awesome list（LLMQuant/awesome-trading-agents、bettyguo/awesome-llm-trading-agents），star 数为当时快照。

## 多 Agent 交易框架（TradingAgents 同类/衍生）
| 项目 | 特点 | Stars |
|------|------|-------|
| virattt/ai-hedge-fund | 14 位传奇投资人 persona（Buffett/Munger/Burry 等）+ 分析 Agent 辩论选股 | ~59k |
| hsliuping/TradingAgents-CN | TradingAgents 中文 A 股 fork：Tushare/AkShare 数据源 + 中文报告 + A 股监管语境 | - |
| KylinMountain/TradingAgents-AShare | A 股重写版，15 个 Agent + 可视化 UI | - |
| FinStep-AI/ContestTrade | Agent 内部先竞争，胜出观点进最终决策 | - |
| HKUDS/AI-Trader | Agent 原生交易平台，任何 Agent 经 SKILL.md 注册实盘交易，多资产+跟单 | - |
| dragon1086/prism-insight | 韩股多 Agent 分析交易，内置 MCP | - |
| CryptoTradingAgents / Circuit Framework | TradingAgents 思路的 crypto 变体（Circuit 为 Apache-2.0 fork，加确定性风控引擎） | - |

## 近亲（不同技术路线）
- **FinRobot**（AI4Finance）— LLM Agent 平台，自动生成股票研究报告；上游为 **FinGPT**（金融 LLM LoRA 微调栈）
- **FinRL** — 深度强化学习路线（15k+），有实盘部署层 FinRL-Trading
- **Qlib + RD-Agent**（微软）— ML 量化全流程 + 自主 alpha 因子发现
- **FinMem** — 分层记忆 + persona 交易，可视为 TradingAgents 的记忆升级版
- **Trading-R1** — 同 Tauric 团队，RL 训练推理链（NVDA Sharpe 2.72，较可信）

## 入口 Awesome List
- LLMQuant/awesome-trading-agents — 按 Agents/MCPs/Skills 分类，专注 LLM 驱动决策（经典量化库见 awesome-quant）
- bettyguo/awesome-llm-trading-agents — 附论文/数据集/基准，对每个项目标注"严谨 vs 炒作"的诚实评估

## 已知局限（以 TradingAgents 为例）
- LLM 训练集泄漏（如 GPT-4o 知道 2024 年初行情）、回测股票池小（7 只 mega-cap，幸存者偏差）
- 新闻情绪延迟 3-20 分钟，HFT 反应 <100ms → 本质适合 swing/波段，不适合日内
- 结论：多 Agent LLM 框架定位是研究/决策辅助，不是自动盈利系统

## 与 A 股数据源的衔接
TradingAgents-CN / AShare 使用 Tushare、AkShare——正好补上 [[public-apis]] 中 A 股数据源的空缺（public-apis 收录的是国际市场 API 为主）。

## 相关页面
- [[trading-agents]] — 锚点项目，多 Agent 辩论架构鼻祖
- [[agent-harness-patterns]] — 多 Agent 专业化分工是 harness 模式在金融域的实践
- [[public-apis]] — 市场数据 API 目录（国际）

> 后续若深挖 ai-hedge-fund / FinRobot（各自 >15k stars），可拆为独立 entity 页。
