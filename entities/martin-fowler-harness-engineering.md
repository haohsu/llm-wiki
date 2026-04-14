---
title: Martin Fowler Harness Engineering 评析
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [person, agent, architecture]
sources: [raw/articles/Harness engineering for coding agent users.md]
---

# Martin Fowler / Thoughtworks Harness Engineering 评析

## 概述

由 Thoughtworks 的 Birgitta Böckeler 撰写，发表在软件工程教父 Martin Fowler 的官方网站上。这是对 Harness Engineering 最具深度的第三方评析，提出了"Feedforward Guides + Feedback Sensors"的心智模型。

## 核心模型

Harness 有三层含义（同心圆）：
1. **模型核心**：被 Harness 的终极对象
2. **编码 Agent 构建者的 Harness**：内置的（系统提示、代码检索机制、编排系统）
3. **编码 Agent 用户的 Harness**：用户为自己的用例构建的外层 Harness

## 两种执行类型

| 类型 | 特征 | 示例 |
| --- | --- | --- |
| **Computational（计算型）** | 确定性、快速、CPU 运行 | 测试、Lint、类型检查、结构分析 |
| **Inferential（推理型）** | 语义分析、GPU/NPU 运行、更慢更贵 | AI 代码审查、LLM-as-judge |

## Feedforward Guides（前馈引导）

提高好结果概率的输入：
- 编码约定（AGENTS.md, Skills）
- 引导脚本
- Code mods（如 OpenRewrite recipes）
- 结构测试

## Feedback Sensors（反馈传感器）

检测问题并触发修正的机制：
- 结构测试（ArchUnit 检查模块边界）
- Review Agent
- 静态分析
- 日志
- 浏览器自动化

## 人的角色：Steer（驾驶）

人的工作是**驾驶** Agent——迭代改进 Harness。每当问题反复出现时，应改进 Feedforward 和 Feedback 控制使其更少发生甚至被阻止。

## 反直觉洞察

> "提升信任度和可靠性需要**约束**解决方案空间，而非扩展它。"

> "团队可能选择最适合'Harness 化'的技术栈，而非最灵活的。"

## 冷静提醒

OpenAI 报告中缺少对功能和行为正确性的验证——这是重要的批判性视角。

## 相关页面
- [[harness-engineering]] — 核心概念
- [[harness-engineering-components]] — 四大支柱
- [[openai-harness-engineering]] — 被评析的 OpenAI 实验
