---
title: Harness Engineering 四大支柱
created: 2026-04-14
updated: 2026-04-14
type: concept
tags: [agent, architecture]
sources: [raw/articles/2026年最火的工程范式来了！Harness 工程（Harness Engineering）到底是什么？—— 10篇顶级文章带你彻底搞懂.md, raw/articles/Harness Engineering The Complete Guide to Building Systems That Make AI Agents Actually Work (2026).md, raw/articles/Harness Engineering Building Systems That Make AI Agents ….md]
---

# Harness Engineering 四大支柱

经过 OpenAI、Anthropic、LangChain、Stripe 等多家公司独立实践后，行业收敛出以下四大支柱。

## 1. 分层上下文架构（Layered Context）

不要把所有指令塞进一个文件。用 AGENTS.md 做目录，指向分层知识源。

### 核心原则
- AGENTS.md 是"目录"，不是"百科全书"（约100行）
- 指向结构化 `docs/` 目录中的深层知识源
- 单体 AGENTS.md 会因上下文拥挤、过度指导、即时腐化而失败

### 推荐目录结构
```
AGENTS.md               ← 目录（~100行）
ARCHITECTURE.md         ← 顶层领域地图
docs/
├── design-docs/        ← 索引化、已验证的架构决策
├── exec-plans/
│   ├── active/
│   ├── completed/
│   └── tech-debt-tracker.md
├── product-specs/
├── references/         ← 为 LLM 重新格式化的外部库文档
└── DESIGN.md, SECURITY.md, etc.
```

### 关键发现
- **仓库外的知识对 Agent 不存在** — Slack 讨论、Google Docs、脑子里的决策必须版本化进仓库
- **渐进式披露（Progressive Disclosure）** — Agent 从稳定入口开始，被教导向哪里看下一步
- OpenAI 项目使用了 88 个 AGENTS.md 文件（每个主要子系统一个）

## 2. Agent 专业化（Agent Specialization）

通用 Agent 上下文容易被污染，专业化子 Agent 保持干净上下文窗口。

### 模式
- **初始化 Agent**：搭建环境（特性列表、git 仓库、进度文件）
- **编码 Agent**：每会话渐进推进
- **测试 Agent / QA Agent / 清理 Agent**：各司其职

### 子 Agent 作为"上下文防火墙"
- 父 Agent 只看到子 Agent 的 prompt 和最终结果
- 中间工具调用、结果等噪音不进入父 Agent 上下文
- 支持成本控制：父用昂贵模型（Opus），子用便宜模型（Sonnet/Haiku）

### 实证
- Anthropic 用 16 个并行 Agent 编译 Linux 内核（10万行代码，$20,000 API 成本）
- 每个 Agent 运行在独立 Docker 容器中，通过裸 git 仓库同步
- 关键发现：更强的模型需要重新设计 Harness 才能发挥新能力

## 3. 持久化记忆（Persistent Memory）

跨会话的进度文件、特性列表、任务状态。

### 核心机制
- **claude-progress.txt**（Anthropic）：跨会话交接，类似轮班工程师交接
- **特性列表（JSON）**：每个功能标记 pass/fail，防止 Agent 过早宣布完成
- **版本化执行计划**（OpenAI）：轻量级临时计划 + 结构化执行计划

### 为什么用 JSON 而非 Markdown
Agent 更不容易不当编辑或覆盖结构化数据。

### 典型会话启动流程
1. `pwd` 确认目录
2. 读 git 日志和进度文件
3. 读特性列表，选择最高优先级未完成特性
4. 运行基本端到端测试确认应用状态
5. 开始工作

## 4. 结构化执行与背压（Structured Execution & Backpressure）

不依赖 LLM 自我验证，用工程手段保证正确性。

### 机械执行层
- **确定性 Linter**：自定义规则自动标记违规
- **架构约束测试**：依赖方向强制执行（如 Types → Config → Repo → Service → Runtime → UI）
- **CI 验证**：代码只能"向前"引用层序列

### 背压机制
- 测试验证器必须近乎完美，否则 Agent 会"解决错误的问题"
- Linter 错误消息设计为**注入修正指令到 Agent 上下文**
- 成功时静默，失败时才产生详细输出（避免上下文窗口被刷满）

### 熵治理（"垃圾回收"）
Agent 大规模生成代码不可避免地积累技术债：
- **文档一致性 Agent**：定期扫描过时文档并开 PR
- **约束违规扫描器**：查找逃过检查的代码
- **模式执行 Agent**：识别和修复偏离既定模式的代码
- **依赖审计器**：跟踪和解决循环或不必要依赖

OpenAI 团队曾每周五花 20% 时间手动清理 AI slop，后来改为后台 Agent 自动化处理。

## 实践层级

### Level 1: 基础 Harness（个人开发者）
- CLAUDE.md / AGENTS.md 项目约定
- Pre-commit hooks (lint + format)
- Agent 可运行的测试套件
- **耗时：1-2 小时**

### Level 2: 团队 Harness（3-10 人）
- 团队级 AGENTS.md
- CI 强制架构约束
- 共享 prompt 模板
- 文档即代码 + Linter 验证
- **耗时：1-2 天**

### Level 3: 生产 Harness（工程组织）
- 自定义中间件（循环检测、推理优化）
- 可观测性集成（Agent 读日志和指标）
- 熵管理 Agent 定时运行
- Harness 版本化和 A/B 测试
- **耗时：1-2 周**

## 相关页面
- [[harness-engineering]] — 核心概念
- [[agent-harness-patterns]] — 实践模式
- [[openai-harness-engineering]] — OpenAI 实施详情
