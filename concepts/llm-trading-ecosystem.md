---
title: LLM 交易 Agent 生态
created: 2026-09-09
updated: 2026-09-10
type: concept
tags: [agent, market, trend, comparison]
sources: [raw/articles/awesome-trading-agents.md, raw/articles/awesome-llm-trading-agents.md, https://github.com/LLMQuant/awesome-trading-agents, https://github.com/bettyguo/awesome-llm-trading-agents]
---

# LLM 交易 Agent 生态

## Overview
以 [[trading-agents]]（2024，LangGraph 多 Agent 辩论架构）为锚点项目的开源生态盘点。2026-09 基于两个 awesome list 的最新版本（LLMQuant/awesome-trading-agents ★448、bettyguo/awesome-llm-trading-agents）更新完成，star 数为 2026-09 快照。

**分层视角**：这个生态可拆为四层——**Agents**（决策主体）、**MCPs**（数据/经纪接入）、**Skills**（Claude Code 等 agent 的可复用交易工作流）、**Benchmarks/方法学**（诚实评估）。awesome-llm-trading-agents 特别强调：投资者必须先读其 `docs/methodology.md`——**漂亮的回测经不起实盘检验是常态**。

## 分层图（2026-09）

```
Agents（决策）
├─ 多 Agent 辩论框架：TradingAgents(104k) / TradingAgents-CN(31.7k) / AShare(817) / ContestTrade / prism-insight / QuantAgent
├─ 单 Agent / persona：ai-hedge-fund(63k，14 投资人 persona) / ValueCell / nof1
└─ 平台 / RL / 其他路线：FinRobot / FinRL / Qlib / FinMem
MCPs（数据/经纪）
├─ 数据：FinanceMCP(664，Tushare+Binance) / mcp-aktools(392，AkShare) / data-mcp / financial-datasets / Yahoo/OpenBB
├─ 经纪/交易所：alpaca-mcp-server(官方) / kraken-cli / metatrader-mcp / IB_MCP / okx-agent-trade-kit
└─ 研究/回测：TradingAgents-MCPmode(335) / maverick-mcp / tradememory-protocol / backtest MCP
Skills（可复用交易工作流）
├─ 权益研究：tradermonty/claude-trading-skills / RKiding/Awesome-finance-skills / JoelLewis/finance_skills(84)
├─ crypto/DeFi：okx / Polymarket / GMGN 官方
└─ 策略编码/回测：vectorbt-backtesting-skills / finlab-ai(台股) / fintool(Rust)
Benchmarks & 方法学
├─ StockBench(2025，contamination-controlled，GPT-5/Claude-4/Qwen3 大多跑不赢 buy-and-hold)
├─ INVESTORBENCH / DeepFund / FinBen / Finova(蚂蚁，含合规维度)
└─ 关键论文：Lookahead Bias(2512.23847) / Deflated Sharpe / PBO(回测过拟合) / AMA(架构>模型)
```

## 多 Agent 交易框架
| 项目 | 特点 | Stars(2026-09) |
|------|------|-------|
| TauricResearch/TradingAgents | 辩论框架鼻祖，LangGraph，analyst+bull/bear+trader+risk+PM | 104,390 |
| hsliuping/TradingAgents-CN | 中文 A 股 fork：Tushare/AkShare + 中文报告 + A 股监管语境 | 31,700 |
| virattt/ai-hedge-fund | 14 位传奇投资人 persona + PM 决断 | 63,323 |
| KylinMountain/TradingAgents-AShare | A 股重写：15 Agent + 美化 UI + Docker 一键部署 | 817 |
| HKUDS/AI-Trader | Agent 原生平台：SKILL.md 注册实盘，多资产+跟单，22.2k | 22,247 |
| HKUDS/Vibe-Trading | 个人多 Agent 金融工作台，A股/HK/美股/crypto/期货/外汇 | - |
| FinStep-AI/ContestTrade | agent 内部竞争，胜出观点进最终决策 | 676 |
| dragon1086/prism-insight | 韩股多 Agent 分析交易，内置 MCP | 741 |
| Y-Research-SBU/QuantAgent | 基于图表图像推理（需视觉 LLM），HFT 研究原型 | 2,853 |
| Tomortec/CryptoTradingAgents | TradingAgents 思路的 crypto 变体 | - |

> 注意：awesome-llm-trading-agents 明确的**诚实评估**——QuantAgent 是 HFT 研究原型（视觉 LLM 推理延迟远超 HFT 决策时域）；任何 2024-25 的 LLM 交易论文都要独立核查评估窗口是否在 LLM 训练截止之后（look-ahead bias）。

## 近亲（不同技术路线）
- **FinRobot**（AI4Finance，7.9k）— LLM Agent 平台，学术风格股票研报；上游 **FinGPT**（21.2k，金融 LLM LoRA 微调栈，本质是 FinLLM toolkit 非交易系统）
- **FinRL** — DRL 路线（16.2k），有 FinRL-X 模块化演进
- **Qlib + RD-Agent**（微软，48.4k）— ML 量化全流程 + 自主 alpha 因子发现
- **FinMem**（pipiku915，957）— 分层记忆 + persona 交易，记忆升级版；论文 arXiv 2311.13743
- **Trading-R1**（Tauric，482，2025-09 未再活跃）— RL 训练 NVDA 推理链，terminal 未发布
- **金融推理 LLM 族**（非交易 agent，作为底座）：Fin-R1（Qwen2.5-7B，FinQA 76.0）、Fino1（Llama-3.1-8B，CoT+RL）、DianJin-R1（阿里云，中文合规语料）、Agentar-Fin-R1（蚂蚁，含 Finova 合规基准）——**别把它们当交易系统**，是 backbone

## 入口 Awesome List
- **LLMQuant/awesome-trading-agents** ★448 — 按 Agents/MCPs/Skills 三块分类，专注 LLM 驱动决策，双语文档（README.zh-CN）
- **bettyguo/awesome-llm-trading-agents** ★5 — 附论文/数据集/基准，对每个项目标注"严谨 vs 炒作"的诚实评估，还带 docs/methodology.md 评估方法论
- 经典量化库（非 LLM agent）不在这两个列表范围内，归 georgezouq/awesome-ai-in-finance、wilsonfreitas/awesome-quant

## 数据源与 MCP 层（A 股衔接）
- **A 股数据**：Tushare / AkShare 生态的项目激增——FinanceMCP（Tushare+Binance，664★，A/HK/美股/基金/债/宏观/新闻）、mcp-aktools（AkShare，392★）、akshare-one-mcp、mcp-cn-a-stock、stock-sdk（TS SDK，A/H/US）、TradingAgents-MCPmode（335★，TradingAgents 改造成 MCP 工具）
- **国际数据**：alpaca-mcp-server（美股/期权官方）、financial-datasets（基本面+价格+新闻）、equibles（自托管数据中枢，SEC/FRED/Yahoo→PostgreSQL）、OpenBB（数据层可审计）
- LLMQuant/data-mcp — "AI-native finance 知识 harness"：50k+ 量化 wiki 语义搜索、SEC 10-K/10-Q 全文、13F 机构持仓三方查询
- 正好补上 [[public-apis]] 的 A 股数据空缺（public-apis 以国际市场为主）

## 诚实评估：能跑赢市场吗
- **StockBench（2025，最可信基准）**：82 个交易日（2025-03-03~06-30），**GPT-5/Claude-4/Qwen3/Kimi-K2/GLM-4.5 大多跑不赢 buy-and-hold**，个别风险调整后有小优势
- **AMA（Agent Market Arena）**：发现**架构 > 模型 backbone 是盈利的主导因素**（若属实，是重磅结论）
- **LAP test（2512.23847）**：LLM 的"预测力"部分来自记忆训练窗口，**回测窗口与 LLM 训练截止重叠即可疑**
- 综合：多 Agent LLM 框架定位是**研究/决策辅助**，不是自动盈利系统；评估任何项目前先读 Deflated Sharpe / PBO（回测过拟合）方法学

## 已知局限（以 TradingAgents 为例）
- LLM 训练集泄漏（如 GPT-4o 知道 2024 年初行情）、回测股票池小（7 只 mega-cap，幸存者偏差）
- 新闻情绪延迟 3-20 分钟，HFT 反应 <100ms → 本质适合 swing/波段，不适合日内
- 大量项目"漂亮的回测经不起实盘"——LLM-Trading-Lab 是少数真金白银（真钱 6 个月微盘实验 + 40 页评估论文）的参照

## 相关页面
- [[trading-agents]] — 锚点项目，多 Agent 辩论架构鼻祖
- [[ai-hedge-fund]] — persona 路线锚点
- [[trading-agents-cn]] / [[trading-agents-ashare]] — A 股 fork 主线
- [[finrobot]] / [[fingpt]] — AI4Finance 平台/model 路线
- [[agent-harness-patterns]] — 多 Agent 专业化分工是 harness 模式在金融域的实践
- [[public-apis]] — 市场数据 API 目录（国际）

> 后续若深挖 ai-hedge-fund / FinRobot（各自 >15k stars）已拆为独立 entity 页；QuantAgent/AI-Trader/FinMem 若再出现可继续拆。单页 200 行内。