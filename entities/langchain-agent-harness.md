---
title: LangChain Agent Harness 实践
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [company, agent, architecture, product]
sources: [raw/articles/The Anatomy of an Agent Harness.md, raw/articles/Harness capabilities.md]
---

# LangChain Agent Harness 实践

## 概述

LangChain 从第一性原理推导 Harness 的每一个组件为什么存在，并用实验证明 Harness 的价值。其核心贡献是定义了 **Agent = Model + Harness** 公式，并证明仅改变 Harness（模型不变）可将基准排名从 Top 30 跃升至 Top 5。

## 核心公式

**Agent = Model + Harness**

- 如果你不是模型，你就是 Harness
- Harness 是模型之外的所有代码、配置和执行逻辑
- 模型包含智能，Harness 让智能变得可用

### Harness 具体包含
- 系统提示
- 工具、Skills、MCP 及其描述
- 基础设施（文件系统、沙盒、浏览器）
- 编排逻辑（子 Agent 生成、交接、模型路由）
- Hooks/Middleware（确定性执行：压缩、延续、Lint 检查）

## 从期望行为推导 Harness 设计

模式：**我们想要的行为 → Harness 设计来帮助模型实现**

### 文件系统 = 持久存储 + 上下文管理
**期望**：Agent 有持久存储来接口真实数据、卸载不适合上下文的信息、跨会话持久化工作

**设计**：Harness 附带文件系统抽象和 fs-op 工具
- Git 添加版本控制：跟踪工作、回滚错误、分支实验
- 文件系统是天然的协作表面

### Bash + 代码 = 通用工具
**期望**：Agent 自主解决问题，不需要人为预设计每个工具

**设计**：Harness 附带 bash 工具
- 模型可自行设计工具（通过代码），而非受限于固定预配置工具集

### 沙盒 + 工具 = 执行和验证环境
**期望**：Agent 在正确默认值的环境中安全行动

**设计**：
- 沙盒提供安全隔离的执行环境
- 预配置语言运行时、包、CLI、浏览器
- 浏览器/日志/截图/测试运行器 → 自验证循环

### 记忆 + 知识注入
**期望**：Agent 记住见过的东西，访问训练时不存在的信息

**设计**：
- AGENTS.md 标准：启动时注入上下文，Agent 编辑后更新 → 持续学习
- Web Search + MCP 工具（如 Context7）突破知识截止日期

## 对抗 Context Rot

Context Rot：上下文窗口填满时模型推理和任务完成能力下降。

### 三大策略
1. **Compaction**：上下文接近满时，智能卸载和总结已有内容
2. **工具调用卸载**：超过阈值的工具输出截断头尾，完整输出存文件系统
3. **Skills**：渐进式披露——模型启动时不加载所有工具描述，按需获取

## 长期自主执行

### 文件系统 + Git
- 持久捕获工作，跟踪长期任务进度
- 多 Agent 共享工作台账

### Ralph Loop
- Hook 拦截模型退出尝试，在新上下文窗口中重新注入原始 prompt
- 强制 Agent 继续工作直到完成

### 规划 + 自验证
- 目标分解为步骤序列
- 完成每步后检查正确性
- Hook 运行预定义测试套件，失败时循环回模型

## 模型训练与 Harness 设计的耦合

### 现状
- Claude Code、Codex 等产品在后训练时带 Harness
- 有用原语被发现 → 加入 Harness → 用于下一代模型训练
- 循环重复：模型在训练时的 Harness 中变得更强大

### 副作用
- 模型可能过度适配其 Harness
- Opus 4.6 在 Claude Code 中排名 #33，但在其他 Harness 中排名 #5
- **最佳 Harness 不一定是模型后训练时的那个**

### Terminal Bench 2.0 实验
- 固定模型 gpt-5.2-codex，仅改进 Harness
- 分数从 52.8% 升至 66.5%（+13.7 分）
- 排名从约 #30 升至约 #5

### 主要改进
| 改动 | 做法 | 效果 |
| --- | --- | --- |
| 自验证循环 | 添加完成前检查清单中间件 | 提交前捕获错误 |
| 上下文工程 | 启动时映射目录结构 | Agent 从一开始就理解代码库 |
| 循环检测 | 跟踪重复文件编辑 | 防止"末日循环" |
| 推理三明治 | 规划/验证用高推理，实施用中推理 | 时间预算内更好质量 |

## Deep Agents 架构（Harness 能力文档）

LangChain 的 Deep Agents harness 提供六大能力：

1. **规划能力**：write_todos 工具维护结构化任务列表
2. **虚拟文件系统**：可插拔后端，支持 ls/read_file/write_file/edit_file/glob/grep/execute
3. **任务委派（Subagent）**：分发子任务
4. **上下文和 token 管理**：Compaction、工具卸载
5. **代码执行**：沙盒环境
6. **人机协作**：Human-in-the-loop

## 未来方向

- 编排数百个并行 Agent 在共享代码库上工作
- Agent 分析自己的 trace 识别和修复 Harness 级失败模式
- Harness 动态按需组装工具和上下文（Just-in-time）

## 相关页面
- [[harness-engineering]] — 核心概念
- [[agent-harness-patterns]] — 实践模式
- [[openai-harness-engineering]] — OpenAI 实践
- [[anthropic-agent-harness]] — Anthropic 实践
