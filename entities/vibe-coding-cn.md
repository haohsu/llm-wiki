---
title: vibe-coding-cn
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, agent, tool, product, strategy]
sources: [https://github.com/tukuaiai/vibe-coding-cn]
---

# Vibe Coding 指南

通过与 AI 结对编程将想法变为现实的终极工作站。中文社区最全面的 Vibe Coding 方法论指南，涵盖道法术器四层体系。

- GitHub: [github.com/tukuaiai/vibe-coding-cn](https://github.com/tukuaiai/vibe-coding-cn)
- Stars: 20,438 | Forks: 2,222
- 语言: Python
- 创建: 2025-12-17
- Telegram: [t.me/glue_coding](https://t.me/glue_coding)
- 多语言: 27 种语言

## 核心理念

> **规划就是一切。** 谨慎让 AI 自主规划，否则你的代码库会变成一团无法管理的乱麻。

Vibe Coding 不是"让 AI 随便写代码"，而是**规划驱动 + 模块化**的 AI 结对编程工作流。

## 元方法论：递归自优化系统

核心思想：构建一个能**自我优化**的 AI 系统。

```
α-提示词（生成器）──→ 生成目标提示词/技能
        ↑                        │
        │     Ω-提示词（优化器）←─┘
        │            │
        └── 优化 ────┘
```

1. **创生** — 用 AI 生成 α-提示词和 Ω-提示词的初始版本
2. **自省与进化** — 用 Ω 优化 α，得到更强的 α-v2
3. **创造** — 用进化后的 α-v2 生成所有目标提示词和技能
4. **循环与飞跃** — 新产物反馈给系统，持续进化

## 道（哲学）

- 凡是 AI 能做的，就不要人工做
- 一切问题问 AI
- 目的主导：一切动作围绕「目的」展开
- 上下文是第一性要素，垃圾进垃圾出
- 先结构后代码，规划好框架
- 奥卡姆剃刀：如无必要，勿增代码
- 帕累托法则：关注重要的 20%
- 逆向思考：先明确需求，从需求逆向构建
- 专注，一次只做一件事

## 法（原则）

- 一句话目标 + 非目标
- 能抄不写，先问 AI 有没有合适的仓库
- 一定要看官方文档，先把官方文档爬下来喂给 AI
- 按职责拆模块
- 接口先行，实现后补
- 一次只改一个模块
- 文档即上下文，不是事后补

## 术（技巧）

- 明确写清：能改什么，不能改什么
- Debug 只给：预期 vs 实际 + 最小复现
- 测试可交给 AI，断言人审
- 代码一多就切会话

## 器（工具链）

### IDE & 终端

| 工具 | 说明 |
|------|------|
| VS Code | 代码阅读与手动修改，Local History 插件 |
| Cursor | AI 编程 IDE |
| Warp | 集成 AI 的现代化终端 |
| Neovim + LazyVim | 键盘流开发者首选 |
| tmux | 终端复用，会话保持 |

### AI 模型分级

| 梯队 | 模型 |
|------|------|
| 第一梯队 | codex-5.1-max-xhigh, claude-opus-4.5-xhigh, gpt-5.2-xhigh |
| 第二梯队 | claude-sonnet-4.5, kimi-k2-thinking, minimax-m2, glm-4.6, gemini-3.0-pro |
| 第三梯队 | qwen3, SWE, grok4 |

### 免费/低价 AI 服务

| 服务 | 说明 |
|------|------|
| Kiro | 免费 Claude Opus 4.5，提供客户端 + CLI |
| Gemini CLI | 免费 Gemini 模型访问 |
| Antigravity | Google 免费 AI，支持 Claude Opus 4.5 + Gemini 3.0 Pro |
| AI Studio | Google 免费，Gemini 3.0 Pro |
| Qwen CLI | 阿里免费额度 |

### 辅助工具

| 工具 | 说明 |
|------|------|
| Augment | 上下文引擎 + 提示词优化 |
| Ollama | 本地大模型管理 |
| Mermaid Chart | 文本转架构图/序列图 |
| NotebookLM | AI 解读资料、生成思维导图 |
| Zread | AI 驱动的 GitHub 仓库阅读 |

## 资源库

| 资源 | 说明 |
|------|------|
| 提示词在线表格 | 数百个可直接复制的提示词 |
| 元提示词库 | 生成提示词的高级提示词 |
| 元技能（Meta-Skill） | 生成 Skills 的 Skill |
| 技能库 | 可直接集成的模块化技能 |
| 系统提示词仓库 | 第三方 AI 工具系统提示词 |
| 通用项目架构模板 | 多种项目类型标准目录结构 |
| prompts-library | Excel ↔ Markdown 提示词转换工具 |

## 与 [[get-shit-done]] 的对比

| 维度 | Vibe Coding 指南 | [[get-shit-done]] |
|------|----------------|------|
| 定位 | AI 编程方法论 + 工具链大全 | Spec 驱动开发系统 |
| 深度 | 道法术器四层哲学 | 六步工作流命令 |
| 工具 | 列举所有主流 IDE/模型/服务 | 专注 Claude Code |
| 社区 | 20k stars + Telegram 群 | 61k stars + Discord |
| 适合场景 | 学习 AI 编程方法论 | 直接上手做项目 |

## 与 [[karpathy-inspired-claude-code-guidelines]] 的关系

Vibe Coding 指南的「术」（明确写清能改什么、Debug 最小复现、断言人审）与 Karpathy 的四大原则（Think Before Coding、Simplicity First、Surgical Changes、Goal-Driven Execution）理念相通，但更偏实操。

## 适用场景

- 学习 AI 编程的完整方法论
- 寻找 AI 编程工具链推荐
- 需要提示词库和 Skills 框架参考
- 中文社区交流和学习

## 局限性

- 内容庞杂，初学者可能无从下手
- 部分链接指向 Google Sheets（需翻墙）
- 经验分享非普遍适用，需辩证采纳
- 模型分级可能随时间变化

## 相关页面

- [[get-shit-done]] — 同类 AI 编程工具，更偏执行
- [[karpathy-inspired-claude-code-guidelines]] — 同类 AI 编程行为准则
- [[knowledge-as-code]] — Vibe Coding 的文档即上下文理念
- [[harness-engineering]] — Vibe Coding 的规划驱动理念
- [[claude-code-skills]] — Vibe Coding 技能库属于此生态
- [[superpowers]] — 同类软件开发方法论
