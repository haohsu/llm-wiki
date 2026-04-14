---
title: Agent Harness 实践模式
created: 2026-04-14
updated: 2026-04-14
type: concept
tags: [agent, architecture, product]
sources: [raw/articles/Effective harnesses for long-running agents.md, raw/articles/Building a C compiler with a team of parallel Claudes.md, raw/articles/The Anatomy of an Agent Harness.md, raw/articles/Skill Issue Harness Engineering for Coding Agents.md]
---

# Agent Harness 实践模式

## 长时运行 Agent 的 Harness 设计（Anthropic）

### 核心挑战
Agent 必须在离散会话中工作，每个新会话开始时没有之前工作的记忆。就像轮班工程师交接——每个新工程师到达时对上一轮班次一无所知。

### 两大失败模式
1. **Agent 试图一次性完成所有工作**：上下文耗尽，下一个会话从半实现的功能开始
2. **后续会话看到部分进展就宣布完成**：过早判定项目完成

### 双 Agent 架构
| Agent | 职责 |
| --- | --- |
| **初始化 Agent** | 搭建环境：特性列表、git 仓库、进度文件、init.sh 脚本 |
| **编码 Agent** | 每会话渐进推进一个特性，留下结构化更新 |

### 关键机制

**特性列表（JSON 格式）**
- 基于用户输入生成详细特性需求（如 claude.ai 克隆：200+ 特性）
- 初始全部标记为 "failing"
- Agent 只能修改 passes 字段，不能删除或编辑测试
- 用 JSON 而非 Markdown（Agent 更不容易不当修改结构化数据）

**增量进度 + Git**
- 每次只做一个特性
- 完成后 commit + 更新进度文件
- 允许 Agent 用 git revert 恢复工作状态

**测试验证**
- Agent 倾向于不做端到端测试就标记完成
- 提供浏览器自动化工具（Puppeteer MCP）进行端到端验证
- 截图对比验证 UI 行为

### 典型会话启动序列
```
pwd → 读进度文件 → 读特性列表 → 读 git 日志 → 启动开发服务器
→ 运行基本端到端测试 → 确认基础功能正常 → 选择下一个特性开始
```

## 多 Agent 并行协作（Anthropic 编译器案例）

### 架构
- 16 个并行 Claude Agent
- 每个 Agent 在独立 Docker 容器中
- 通过裸 git 仓库同步
- ~2000 次会话，$20,000 API 成本
- 产出：10 万行 Rust C 编译器，可编译 Linux 6.9 内核

### 关键设计
- **任务锁机制**：Agent 通过写入文本文件"锁定"任务
- **Ralph Loop**：Agent 完成任务后立即拾取下一个，循环运行
- **测试作为验证器**：测试验证器必须近乎完美

### 经验教训
- Agent 无法感知时间流逝（"时间盲"），Harness 需控制进度打印和测试采样
- 更强的模型（如 Opus 4.6 vs 4.5）需要重新设计 Harness

## Harness 五大战术组件（HumanLayer 视角）

Harness Engineering 是 [[harness-engineering-vs-context-engineering|Context Engineering]] 的子集，专注于利用 Harness 配置点管理编码 Agent 的上下文窗口。

### 1. Skills（技能）
- **渐进式披露**：Agent 只在需要时获取特定指令/知识/工具
- 可以打包 CLI 工具、模板、参考文档
- **安全警告**：已有恶意 Skill 分发案例，需谨慎对待第三方注册表

### 2. MCP 服务器
- 标准化工具集成协议
- 工具定义消耗 token——连接太多 MCP 工具会让 Agent 变笨
- 如果 CLI 在训练数据中有良好表示，优先用 CLI 而非 MCP
- Anthropic 实验性支持 MCP 工具搜索（渐进式披露工具）

### 3. 子 Agent（上下文防火墙）
- 父 Agent 只看到 prompt 和最终结果，中间噪音不进入上下文
- 避免 Context Rot：Chroma 研究证实性能随上下文长度增加而下降
- 支持成本控制：父用 Opus，子用 Sonnet/Haiku
- 适用场景：代码库分析、信息流追踪、代码/文档/网页研究

### 4. Hooks（钩子）
- 确定性触发的自动化动作
- 用例：通知、审批、集成（Slack/PR）、验证（typecheck/build）
- 原则：成功时静默，失败时才产生输出

### 5. 背压机制
- Agent 成功解决问题的概率与自验证能力正相关
- Typecheck、单元测试、集成测试、代码覆盖率、UI 测试
- **关键**：验证机制必须上下文高效——成功吞掉输出，只暴露错误

## Harness 设计的抽象层级（Phil Schmid 视角）

用计算机类比：
- **模型 = CPU**：原始处理能力
- **上下文窗口 = RAM**：有限的易失性工作内存
- **Agent Harness = 操作系统**：管理上下文、处理启动序列、提供标准驱动
- **Agent = 应用**：运行在 OS 之上的具体用户逻辑

## "苦涩教训"的生存法则

Rich Sutton 的"苦涩教训"在 Agent 开发中重演：
- Manus 6 个月内重构 Harness 5 次
- LangChain 一年内重构 Open Deep Research 3 次
- Vercel 移除 80% Agent 工具

**Harness 必须轻量化**。2024 年需要复杂手工管道的能力，2026 年可能只需单一上下文窗口。过度工程化的 Harness 在模型升级时会崩溃——必须保持"可撕裂"设计。

## 相关页面
- [[harness-engineering]] — 核心概念
- [[harness-engineering-components]] — 四大支柱
- [[anthropic-agent-harness]] — Anthropic 详细实践
- [[langchain-agent-harness]] — LangChain 实践
