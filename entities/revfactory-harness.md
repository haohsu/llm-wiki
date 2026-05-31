---
title: Harness
created: 2026-05-31
updated: 2026-05-31
type: entity
tags: [agent, tool, open-source, prompt-engineering]
sources: [https://github.com/revfactory/harness]
---

# Harness

- **GitHub**: https://github.com/revfactory/harness
- **Stars**: 4.4k
- **作者**: revfactory (Hwang, M.)
- **版本**: 1.2.0
- **License**: Apache-2.0
- **定位**: Claude Code 团队架构工厂（Team-Architecture Factory），L3 元工厂层

## 概述

Harness 是 Claude Code 的插件，用于自动生成 Agent 团队架构和技能。用户只需说「build a harness for this project」，插件会根据领域描述，从 6 种预定义的团队架构模式中选择最合适的，自动生成 `.claude/agents/` 和 `.claude/skills/` 目录下的 Agent 定义和技能文件。

## 六大架构模式

| 模式 | 说明 | 适用场景 |
|------|------|----------|
| Pipeline | 顺序依赖任务 | 多阶段流水线 |
| Fan-out/Fan-in | 并行独立任务 | 多维度并行分析 |
| Expert Pool | 按上下文选择性调用 | 领域专家按需协作 |
| Producer-Reviewer | 生成 + 质量审查 | 内容生产+审核 |
| Supervisor | 中央 Agent 动态分发任务 | 复杂协调场景 |
| Hierarchical Delegation | 自顶向下递归委派 | 大型项目分解 |

## 核心特性

- **Agent 团队设计**: 根据领域描述自动选择架构模式并生成团队配置
- **技能生成**: 自动生成带 Progressive Disclosure 的技能文件，优化上下文管理
- **编排协议**: Agent 间数据传递、错误处理、团队协调协议
- **验证体系**: 触发验证、dry-run 测试、有/无技能对比测试

## 工作流程

```
Phase 1: 领域分析
    ↓
Phase 2: 团队架构设计（Agent Teams vs Subagents）
    ↓
Phase 3: Agent 定义生成（.claude/agents/）
    ↓
Phase 4: 技能生成（.claude/skills/）
    ↓
Phase 5: 集成与编排
    ↓
Phase 6: 验证与测试
```

## 实验数据

A/B 测试（n=15，作者自测）显示：

| 指标 | 无 Harness | 有 Harness | 提升 |
|------|:---------:|:---------:|:----:|
| 平均质量分 | 49.5 | 79.3 | **+60%** |
| 胜率 | — | — | **100%** (15/15) |
| 输出方差 | — | — | **-32%** |

效果随任务复杂度递增：基础 +23.8，进阶 +29.6，专家 +36.2。

> 注：数据来自作者自测（n=15），第三方复现待验证。

## 生态定位

Harness 位于 Claude Code 生态的 **L3 元工厂层**——生成其他 Harness 而非本身是 Harness：

| 层级 | 功能 | 同层项目 |
|------|------|----------|
| **L3 元工厂 / 团队架构工厂** (Harness) | 领域描述 → Agent 团队 + 技能，6 种架构模式 | — |
| L3 元工厂 / 运行时配置工厂 | 确定性、可重复的运行时配置 | [[archon]] |
| L3 元工厂 / Codex 运行时移植 | 同概念的 Codex 版本 | meta-harness |
| L2 跨 Harness 工作流 | 跨 Harness 标准化 skills/rules/hooks | ECC |

## 关联项目

- **harness-100**: 100 个生产级 Agent 团队 Harness，覆盖 10 个领域（英/韩双语，1,808 个 Markdown 文件）
- **claude-code-harness**: A/B 实验仓库，15 个软件工程任务的对比测试
- 与 [[harness-engineering]] 概念互补：Harness 是工具实现，Harness Engineering 是工程范式
- 与 [[superpowers]] 理念相近：都强调对 Agent 行施的强制约束

## 局限

- 仅支持 Claude Code（Codex 版本由社区维护的 meta-harness 提供）
- 需要启用实验性 Agent Teams 功能 (`CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`)
- +60% 数据为小样本作者自测，尚无第三方独立复现
- 依赖 Claude Code 原生能力，不适用于其他 LLM 框架（如 LangGraph）
