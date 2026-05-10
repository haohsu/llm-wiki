---
title: addyosmani/agent-skills
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, agent, tool, product]
sources: [https://github.com/addyosmani/agent-skills]
---

# Addy Osmani Agent Skills

Google Chrome 团队工程师 Addy Osmani 开源的生产级 AI 编程 Agent 技能包，将资深工程师的工作流程编码为 Agent 可执行的结构化工作流。

- GitHub: [github.com/addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)
- 许可: MIT
- 技能数: 22（21 个生命周期技能 + 1 个元技能）
- 作者: Addy Osmani（Google Chrome 工程师，《Learning JavaScript Design Patterns》等书作者）
- 定位: 将 Google 工程文化编码为 Agent 可执行的工作流

## 核心理念

AI 编程 Agent 默认走最短路径——跳过 Spec、测试、安全审查等保障软件可靠性的实践。Agent Skills 为 Agent 提供结构化工作流，强制执行资深工程师的纪律。

**四大设计原则：**
- **流程而非散文** — 技能是 Agent 遵循的工作流，不是参考文档
- **反合理化** — 每个技能包含 Agent 常用借口的反驳表（如"我之后再加测试"）
- **验证不可协商** — 每个技能以证据要求结束，"看起来对"永远不够
- **渐进式披露** — SKILL.md 是入口，支持性引用按需加载，最小化 token 消耗

## 开发生命周期

```
DEFINE → PLAN → BUILD → VERIFY → REVIEW → SHIP
 /spec   /plan   /build   /test    /review   /ship
```

## 7 个斜杠命令

| 命令 | 用途 | 核心原则 |
|------|------|----------|
| /spec | 定义要构建什么 | 先 Spec 后 Code |
| /plan | 规划如何构建 | 小而原子的任务 |
| /build | 增量构建 | 一次一个切片 |
| /test | 证明它能工作 | 测试即证明 |
| /review | 合并前审查 | 改善代码健康 |
| /code-simplify | 简化代码 | 清晰优于聪明 |
| /ship | 部署到生产 | 更快即更安全 |

## 22 个技能

### Meta
- using-agent-skills — 将工作映射到正确的技能工作流，定义共享操作规则

### Define（定义）
- idea-refine — 结构化发散/收敛思考，将模糊想法变成具体提案
- spec-driven-development — 在写代码前写 PRD（目标、命令、结构、代码风格、测试、边界）

### Plan（规划）
- planning-and-task-breakdown — 将 Spec 分解为小的、可验证的任务，带验收标准和依赖排序

### Build（构建）
- incremental-implementation — 薄垂直切片：实现→测试→验证→提交，特性标志、安全默认值
- test-driven-development — 红-绿-重构，测试金字塔（80/15/5），DAMP 优于 DRY，Beyonce 规则
- context-engineering — 在正确的时间给 Agent 正确的信息
- source-driven-development — 每个框架决策都基于官方文档验证、引用来源
- doubt-driven-development — 对抗性新鲜上下文审查：CLAIM→EXTRACT→DOUBT→RECONCILE→STOP
- frontend-ui-engineering — 组件架构、设计系统、状态管理、响应式设计、WCAG 2.1 AA
- api-and-interface-design — 契约优先设计、Hyrum 法则、One-Version 规则、错误语义

### Verify（验证）
- browser-testing-with-devtools — Chrome DevTools MCP 进行实时运行时数据检查
- debugging-and-error-recovery — 五步分诊：复现→定位→缩减→修复→防护

### Review（审查）
- code-review-and-quality — 五轴审查、变更大小（~100 行）、严重性标签
- code-simplification — Chesterton 栅栏、500 行规则，降低复杂度同时保留行为
- security-and-hardening — OWASP Top 10 防护、认证模式、密钥管理、依赖审计
- performance-optimization — 测量优先：Core Web Vitals 目标、分析工作流

### Ship（发布）
- git-workflow-and-versioning — 主干开发、原子提交、变更大小（~100 行）
- ci-cd-and-automation — Shift Left、更快即更安全、特性标志、质量门流水线
- deprecation-and-migration — 代码即负债、强制 vs 建议弃用、迁移模式
- documentation-and-adrs — 架构决策记录、API 文档、记录"为什么"
- shipping-and-launch — 上线清单、特性标志生命周期、分阶段发布、回滚程序

## 3 个 Agent 角色

| 角色 | 定位 | 核心能力 |
|------|------|----------|
| code-reviewer | 资深 Staff 工程师 | 五轴代码审查，"Staff 工程师会批准吗？"标准 |
| test-engineer | QA 专家 | 测试策略、覆盖率分析、Prove-It 模式 |
| security-auditor | 安全工程师 | 漏洞检测、威胁建模、OWASP 评估 |

## 4 个参考清单

- testing-patterns.md — 测试结构、命名、Mock、React/API/E2E 示例
- security-checklist.md — 预提交检查、认证、输入验证、CORS、OWASP Top 10
- performance-checklist.md — Core Web Vitals 目标、前后端清单
- accessibility-checklist.md — 键盘导航、屏幕阅读器、ARIA、测试工具

## Google 工程文化编码

技能中嵌入了 Google 工程实践的核心概念：

| 概念 | 出处 | 应用技能 |
|------|------|----------|
| Hyrum 法则 | SWE at Google | api-and-interface-design |
| Beyonce 规则 | Google eng-practices | test-driven-development |
| 测试金字塔 | SWE at Google | test-driven-development |
| 变更大小（~100 行） | Google eng-practices | code-review-and-quality, git-workflow |
| Chesterton 栅栏 | 经典原则 | code-simplification |
| 主干开发 | Google eng-practices | git-workflow-and-versioning |
| Shift Left | DevOps 最佳实践 | ci-cd-and-automation |

## 多平台兼容

支持 Claude Code（推荐）、Cursor、Gemini CLI、Windsurf、OpenCode、GitHub Copilot、Kiro、Codex 等所有主流 AI 编程工具。

## 与其他技能包的对比

| 维度 | agent-skills | [[baoyu-skills]] | [[superpowers]] |
|------|-------------|------------------|-----------------|
| 定位 | 软件工程全流程 | 内容生成+AI 工具链 | 开发方法论编码 |
| 技能数 | 22 | 60+ | 多模块 |
| 核心价值 | Google 工程文化 | 多平台发布 | 研究→计划→执行 |
| 特色 | 反合理化机制 | 中文生态 | 渐进式构建 |

## 生态关系

- 与 [[superpowers]] 同属开发方法论类技能，但更聚焦 Google 工程实践
- 与 [[baoyu-skills]] 互补——baoyu 偏内容生成，agent-skills 偏软件工程
- 与 [[claude-code-skills]] 生态深度集成，支持 Claude Code 插件市场安装
- 与 [[mattpocock-skills]] 理念相近——都关注修复 Agent 的失败模式
