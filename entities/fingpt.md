---
title: FinGPT
created: 2026-09-10
updated: 2026-09-10
type: entity
tags: [model, open-source, fine-tuning]
sources: [raw/articles/awesome-llm-trading-agents.md]
---

# FinGPT

- **GitHub**: https://github.com/AI4Finance-Foundation/FinGPT
- **Stars**: 21,233（2026-09 快照）
- **活跃度**: 2026-09-08 有 push
- **组织**: AI4Finance Foundation

## 是什么

AI4Finance 的开源**金融大语言模型栈**（FinLLM 微调，非交易系统）：

- FinGPT v3 系列：LoRA 微调 Llama-2（7B/13B）、ChatGLM2（6B），训练语料为新闻/推文情绪数据
- 配套 FinNLP pipeline：金融领域专用微调流水线
- 广泛引用的"~$300 微调成本"指**小数据量 LoRA 调优**，不适用于从零构建金融 LLM

## 诚实评估（来自 awesome-llm-trading-agents）

- 本质是 **FinLLM toolkit / 微调 LM**，不是独立交易 agent
- 被 [[finrobot]] 等下游 agent 平台用作情绪打分的底座
- LLM-trading 栈里通常从 FinGPT 起步做 sentiment scoring

## 相关页面

- [[FinRobot]] — 同门上层 agent 平台
- [[llm-trading-ecosystem]] — 技术路线近亲一节
- [[trading-agents]] — 辩论制框架对照