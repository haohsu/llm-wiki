---
title: Harness Engineering
created: 2026-04-14
updated: 2026-04-14
type: concept
tags: [agent, architecture, trend]
sources: [raw/articles/2026年最火的工程范式来了！Harness 工程（Harness Engineering）到底是什么？—— 10篇顶级文章带你彻底搞懂.md, raw/articles/Beyond Prompts and Context Harness Engineering for AI Agents.md, raw/articles/Harness Engineering Building Systems That Make AI Agents ….md]
---

# Harness Engineering

## 定义

Harness Engineering 是 2026 年初兴起的工程范式，指围绕 AI Agent 设计约束、反馈循环、文档结构、Linting 规则、可观测性管道和生命周期管理系统，使 Agent 能在大规模下可靠运行的学科。

**核心公式：Agent = Model + Harness**

- **Model（模型）= 马**：强大、快速，但自己不知道往哪跑
- **Harness（缰绳系统）= 约束+反馈+工具编排+生命周期管理**：让智能变得可用
- **工程师 = 骑手**：不再亲自写代码，而是设计让 Agent 可靠写代码的「环境」

词源来自马术——缰绳、马鞍、嚼子——一整套用来驾驭强壮但不可预测动物的装备。

## 诞生时间线

| 时间 | 事件 | 关键人物 |
| --- | --- | --- |
| 2025年11月 | Anthropic 发布长时 Agent Harness 工程报告 | Anthropic 工程团队 |
| 2026年1月 | Phil Schmid 预言"Agent Harness 将定义2026年" | Phil Schmid |
| 2026年2月5日 | Mitchell Hashimoto 首次命名"Harness Engineering" | HashiCorp 联合创始人 |
| 2026年2月11日 | OpenAI 发布百万行代码实验报告，标题使用"Harness Engineering" | OpenAI Codex 团队 |
| 2026年2月17日 | Martin Fowler 网站发布权威评析 | Birgitta Böckeler / Thoughtworks |
| 2026年3月 | LangChain 发布"Agent Harness 解剖学" | LangChain 团队 |

## 原始定义（Mitchell Hashimoto）

> "每次 Agent 犯错时，你花时间设计一个解决方案，确保 Agent 永远不会再犯同样的错误。"

这是 Harness Engineering 运动的概念起点，来自 HashiCorp 联合创始人 Mitchell Hashimoto 在 Ghostty 项目中的实践。他的 AGENTS.md 文件中每一行都代表一个过去的 Agent 失败案例及其防范规则。

## 工程师角色的转变

| 传统软件工程 | Harness Engineering |
| --- | --- |
| 写代码 | 设计 Agent 运行的环境 |
| 调试代码 | 调试 Agent 行为模式 |
| 审查代码 | 审查 Agent 输出 + Harness 有效性 |
| 写测试 | 设计测试策略供 Agent 执行 |
| 维护文档 | 构建机器可读的文档基础设施 |

**核心转变**：从"生产正确代码"到"生产让 Agent 可靠产出正确代码的环境"。

## 稀缺性反转

传统开发中，计算便宜，人的注意力中等稀缺。Agent-first 环境中，代码吞吐量激增，瓶颈变为人的 QA 能力。**稀缺资源变为人的注意力**。这改变了所有工程权衡：等待昂贵，修正便宜。

## 关键实验证据

### OpenAI：百万行代码，零行手写
- 5个月，3→7名工程师，~1500 PR，~100万行代码
- 速度约为人工开发的 10 倍
- 关键：初始效果差，随着 Harness 改进而急剧提升

### Hashline：仅改编辑格式，6.7% → 68.3%
- 安全研究员 Can Boluk 的实验
- 给每行加 2-3 字符 hash，让模型通过 hash 引用行而非精确文本
- Grok Code Fast 1 基准分数从 6.7% 跳到 68.3%
- **模型权重未变，只变了 Harness**

### LangChain：Top 30 → Top 5
- 固定模型 gpt-5.2-codex，仅改进 Harness
- Terminal Bench 2.0 分数从 52.8% 升至 66.5%
- 主要改进：自验证循环、上下文工程、循环检测

## 与其他概念的关系

| 概念 | 关注问题 | 典型场景 |
| --- | --- | --- |
| [[harness-engineering-vs-context-engineering#Prompt Engineering\|Prompt Engineering]] | "怎么措辞？" | 单次交互优化 |
| [[harness-engineering-vs-context-engineering\|Context Engineering]] | "模型看到什么？" | 管理上下文窗口中的全部信息 |
| Harness Engineering | "系统阻止、度量和修复什么？" | Agent 运行环境的完整生命周期 |

**关系：Harness Engineering ⊃ Context Engineering ⊃ Prompt Engineering**

## 核心洞察

1. **模型是大宗商品，Harness 才是护城河** — 模型性能趋同（Claude、GPT、Gemini），Harness 是各团队必须自己构建的资产
2. **约束解决方案空间反而提升效率** — 反直觉：限制 Agent 的行动范围让它更快收敛到正确解
3. **Harness 需要"可撕裂"设计** — 过度工程化的 Harness 在模型升级时会崩溃
4. **投资复利效应** — 每次 Harness 改进都适用于未来所有 Agent 运行

## 相关概念
- [[harness-engineering-components]] — 四大支柱详解
- [[harness-engineering-vs-context-engineering]] — 与 Context/Prompt Engineering 辨析
- [[agent-harness-patterns]] — 实践模式
- [[openai-harness-engineering]] — OpenAI 实验详情
- [[anthropic-agent-harness]] — Anthropic 实践
- [[langchain-agent-harness]] — LangChain 实践
