---
title: A 股交易决策技术路线
created: 2026-09-10
updated: 2026-09-10
type: concept
tags: [market, strategy, comparison, trend]
sources: [raw/articles/awesome-trading-agents.md, raw/articles/awesome-llm-trading-agents.md]
---

# A 股交易决策技术路线

> 面向 A 股（沪深）场景的决策技术路线盘点与取舍。结论先行：**推荐"LLM × 量化混合"（路线 E）为主轴，多智能体作为研究层，ML 做预测补充**；直接让 LLM 全自动下单不推荐。

## 一、A 股结构特征（所有路线的前提）

1. **T+1 + 涨跌停 + 停牌**：当日买入不可卖，一字板/跌停无法成交 → 高频/日内天然受限，回测里"涨停价可成交"是幻觉
2. **散户主导 + 政策市**：量价情绪、资金流、龙虎榜、北向资金影响大 → 非结构化信息价值高，题材轮动是主要收益来源之一
3. **数据分层**：日线/财报 Tushare、AkShare 免费可得；分钟级/Level-2/逐笔贵且基本不对个人开放；复权、停牌、财报对齐全是坑
4. **监管**：程序化交易新规（高频需报告/差异化收费）、券商接口合规限制 → 个人实盘自动化门槛高；退市常态化，ST 风险逻辑与美股不同

结论：所有现实方案在**日线/分钟级、swing 至波段区间**竞争；纯 HFT / 纯日内路线直接放弃。

## 二、五条路线与取舍

| 路线 | 玩法 | 代表 | 选它的原因 | 不选/限制 |
|------|------|------|-----------|-----------|
| **A 传统量化多因子** | Barra/量价/基本面因子 + 打分 + 组合优化 | Qlib（微软，48k★，原生 A 股数据）、聚宽/米筐 | 散户占比高 → 量价/反转/换手因子 alpha 空间比美股大；全流程可回测、可解释、合规透明，是唯一能稳定存活的底座 | 因子拥挤衰减快；纯基本面受财报造假/ST 拖累；读不懂新闻，抓不到题材轮动 |
| **B 机器学习预测** | 特征工程（量价+资金流+情绪代理）→ GBDT/LSTM/Transformer → 预测收益 | XGBoost 系、Qlib 自带模型 | A 股信噪比低，非线性模型挖交互特征；适合做"预测层"输出给仓位/风控 | 纯 ML 回测漂亮实盘崩是常态，必须套 PBO / Deflated Sharpe 防过拟合（见 [[llm-trading-ecosystem]] 诚实评估）；对政策/消息无感知 |
| **C 强化学习** | state=行情+持仓，action=买卖/仓位，reward=收益-风险 | FinRL | 组合再平衡、仓位管理这类连续决策问题天然适合 | T+1/涨跌停使动作空间要深度定制；样本效率低、模拟与现实 gap 大；FinRL 教程收益基本不可复现；做执行层辅助尚可，别端到端 |
| **D LLM 多智能体决策** | LLM 读新闻/公告/研报/舆情，分析师+多空研究员辩论，PM 拍板 | [[trading-agents]]（104k★）、[[trading-agents-cn]]（31.7k★，中文 A 股 fork）、[[ai-hedge-fund]]（63k★，投资人 persona） | 完美匹配政策市+消息市：降准/产业政策/龙虎榜全是非结构化文本，LLM 最擅长；中文语料 DeepSeek/Qwen/GLM 便宜且强 | StockBench 实测主流 LLM 直接决策大多跑不赢 buy-and-hold；训练集泄漏→幻影 alpha（LAP test）；新闻情绪延迟 3-20 分钟 → 只能研究/决策辅助，不能当执行系统 |
| **E LLM × 量化混合（推荐）** | 双层：LLM 读公告/新闻/龙虎榜 → 输出情绪分数/事件标签/alpha 因子；量化层因子合成 → 打分选股 → 仓位/风控/执行 | Qlib+RD-Agent、AlphaGen（RL 式 alpha 因子生成 + LLM 侧通道）、FinRobot 类平台 | 各取所长：LLM 做语义理解（信息→特征），量化做可复现决策（特征→交易）；LLM 产出变成"可回测的因子"，绕开 D 不可验证的问题，LLM 观点飘了量化层风控兜底；A 股政策新闻密集、舆情噪声大，正好需要语义清洗+结构化 | 工作量最大：因子库、回测框架、数据管线三件套要自己搭 |

## 三、推荐组合（路线 E 展开）

1. **数据层**：Tushare/AkShare 日线 + 财报 + 龙虎榜；新闻用财经 API（东财/财联社）——补上 [[public-apis]] 的 A 股空缺
2. **研究层（LLM）**：多 Agent 辩论改造成"事件/情绪打分器"——不直接下单，输出结构化信号（多空分、事件标签、置信度）
3. **量化层**：Qlib 做因子回测底座 + XGBoost 预测层 + 简单仓位规则（Kelly 半仓、最大回撤熔断）
4. **风控**：涨跌停/停牌过滤、单票上限、程序化交易合规检查
5. **评价**：强制 StockBench 式样本外验证 + PBO 校正；LLM 特征单独做消融，证明真加了分

## 四、相关页面

- [[llm-trading-ecosystem]] — LLM 交易 Agent 生态总览（四层框架、诚实评估基准 StockBench/AMA/LAP test）
- [[trading-agents-cn]] — 中文 A 股 fork，路线 D/E 的现成实现基础（即用户所在仓库）
- [[trading-agents]] / [[ai-hedge-fund]] — 多 Agent 辩论 / persona 决策锚点
- [[finrobot]] / [[fingpt]] — 平台 / FinLLM 底座路线
- [[agent-harness-patterns]] — 多 Agent 专业化分工是 harness 模式在金融域的实践
- [[public-apis]] — 国际市场数据 API 目录（A 股空缺对照）

> 本页为综合既有 wiki 内容 + 两个 awesome list 的原始分析，非单一来源 ingest。后续若有实战落地（TradingAgents-CN 改造为研究层），可在此页追加案例。