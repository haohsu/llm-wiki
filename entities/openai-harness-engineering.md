---
title: OpenAI Harness Engineering 实验
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [company, agent, architecture, product]
sources: [raw/articles/2026年最火的工程范式来了！Harness 工程（Harness Engineering）到底是什么？—— 10篇顶级文章带你彻底搞懂.md, raw/articles/Harness Engineering Building Systems That Make AI Agents ….md, raw/articles/The Emerging Harness Engineering Playbook.md]
---

# OpenAI Harness Engineering 实验

## 概述

2026 年 2 月，OpenAI 的 Ryan Lopopolo 发布了"Harness Engineering"实践报告，记录了一个小型团队在五个月内用 Codex Agent 构建约百万行代码产品的实验。所有源码均由 Agent 编写，零行人工手写。这是"Harness Engineering"一词最具影响力的实践报告。

## 实验数据

| 指标 | 数据 |
| --- | --- |
| 周期 | 2025.08 ~ 2026.01（约 5 个月） |
| 团队规模 | 3 → 7 名工程师 |
| 手写代码 | 0 行 |
| 生成代码 | ~100 万行 |
| 合并 PR | ~1500 个 |
| 平均 PR/天/人 | 3.5 个 |
| 速度估计 | 约为人工开发的 10 倍 |

## 三大支柱

### 1. 上下文工程

**AGENTS.md 策略**
- AGENTS.md 是"目录"（~100行），不是"百科全书"
- 指向 `docs/` 目录中的深层知识源
- 使用 88 个 AGENTS.md 文件（每个主要子系统一个）
- 背景 Agent 定期扫描过时文档并开清理 PR

**单体 AGENTS.md 的四大失败原因**
1. 上下文拥挤：大指令文件挤掉任务、代码和相关文档
2. 过度指导导致无指导：所有内容标记为重要时，Agent 停止遵循规则
3. 即时腐化：单体手册无法机械验证，成为过时规则的墓地
4. 不可检测的漂移：没有结构验证，任何文档都会静默衰减

### 2. 架构约束

**分层领域架构**
```
Types → Config → Repo → Service → Runtime → UI
```
- 每层只能"向前"引用序列中的层
- 跨切关注点（auth、连接器、遥测、功能标志）只能通过 Providers 进入
- Linter 本身由 Codex 生成

**额外约束**
- 结构化日志
- Schema 和类型的命名约定
- 文件大小限制
- 平台特定可靠性要求
- 所有外部边界的数据验证

### 3. 熵治理（"垃圾回收"）

**问题**：Agent 大规模生成代码会忠实复制代码库中的模式（包括坏模式），导致漂移和不一致——"AI slop"

**初始方案**：每周五花 20% 时间手动清理 → 不可扩展

**解决方案**："黄金原则" + 后台 Agent
- 优先使用共享工具包而非手写 helper
- 在边界验证数据而非推测性探测
- 使用团队的 OpenTelemetry 工具化并发工具

后台 Codex 任务定期扫描偏差、更新质量评分、开定向重构 PR。

## 应用可读性

Agent 吞吐量扩展后发现瓶颈：Agent 看不到运行中的应用。

### 解决方案
- **Per-worktree 启动**：每个 git worktree 可独立启动应用，消除并发 Agent 间的环境污染
- **Chrome DevTools Protocol 集成**：DOM 截图、浏览器导航，让 Agent 可直接驱动 UI 验证
- **临时本地可观测性栈**：每个 worktree 独立的日志/指标/追踪管道

### 自主开发循环
给定单一 prompt，Agent 可以：
1. 验证代码库状态 → 2. 复现 bug → 3. 录制失败视频 → 4. 实施修复 → 5. 驱动应用验证 → 6. 录制修复视频 → 7. 开 PR → 8. 响应反馈 → 9. 修复构建失败 → 10. 合并

## 知识管理

### 计划作为一等仓库构件
- 执行计划版本化存储在仓库中
- 后续任务的 Agent 可推理之前任务的决策和理由
- 活跃计划、完成计划、技术债追踪器都版本控制

### 文档 Linter
- 专用 Linter 验证知识库交叉链接和结构
- CI 任务检查文档相对于代码的新鲜度
- "文档园艺" Agent 定期扫描过时文档

## 合并哲学

- 最小化阻塞合并门
- PR 短生命周期
- 测试 flake 用后续运行处理而非无限阻塞
- **逻辑**：Agent 吞吐量远超人工注意力时，修正便宜，等待昂贵

## 关键引述

> "仓库外的知识对 Agent 来说不存在——Slack 讨论、Google Docs、脑子里的决策，统统要版本化进仓库。"

> "当 Agent 遇困时的黄金法则：从不回答'再试一次'，而是问'缺少什么能力，如何让它对 Agent 既可读又可执行？'"

## 相关页面
- [[harness-engineering]] — 核心概念
- [[harness-engineering-components]] — 四大支柱
- [[anthropic-agent-harness]] — Anthropic 实践对比
