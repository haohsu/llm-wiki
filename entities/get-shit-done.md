---
title: get-shit-done
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, agent, tool, product, strategy]
sources: [https://github.com/gsd-build/get-shit-done, https://raw.githubusercontent.com/gsd-build/get-shit-done/main/README.md]
---

# GET SHIT DONE (GSD)

轻量级元提示（meta-prompting）、上下文工程与 Spec 驱动开发系统，由独立开发者 TÂCHES 创建。核心解决 AI 编程中的 **上下文腐烂**（context rot）问题——随着会话增长，AI 输出质量下降。

- GitHub: [github.com/gsd-build/get-shit-done](https://github.com/gsd-build/get-shit-done)
- npm: `npx get-shit-done-cc@latest`
- Stars: 61,164 | Forks: 5,191
- 语言: JavaScript
- 许可: MIT
- 创建: 2025-12-14
- 作者: TÂCHES（独立开发者）
- Discord: [discord.gg/mYgfVNfA2r](https://discord.gg/mYgfVNfA2r)

## 核心理念

> "I'm a solo developer. I don't write code — Claude Code does."

其他 Spec 驱动工具面向 50 人工程团队（sprint、story points、Jira），GSD 面向独立创作者。复杂度在系统内部，用户只看到几个"就是能用"的命令。

## 六步工作流

| 命令 | 作用 |
|------|------|
| `/gsd-new-project` | 提问 → 调研 → 需求 → 路线图 |
| `/gsd-discuss-phase [N]` | 在规划前捕获实现决策（布局、API 形状、错误处理等） |
| `/gsd-plan-phase [N]` | 调研 + 规划 + 验证循环，直到计划通过 |
| `/gsd-execute-phase <N>` | 并行执行计划，每个执行器获得全新的 200k token 上下文 |
| `/gsd-verify-work [N]` | 验收测试，失败项生成诊断修复计划 |
| `/gsd-ship [N]` | 从已验证的工作创建 PR |

辅助命令：`/gsd-progress --next`（自动检测下一步）、`/gsd-complete-milestone`（归档里程碑）、`/gsd-new-milestone`（开始下一版本）。

## 解决的三个核心问题

1. **上下文膨胀** — 主上下文保持在 30-40%，重活在全新 subagent 上下文中完成
2. **无共享记忆** — 通过结构化制品（PROJECT.md / REQUIREMENTS.md / ROADMAP.md / STATE.md / CONTEXT.md）跨越会话边界
3. **无验证** — verify 步骤用专用 debug agent 诊断失败，生成修复计划后再执行

## 多 Agent 编排

```
主上下文（30-40%）
  ├─ Researcher subagent（全新上下文）
  ├─ Planner subagent（全新上下文）
  ├─ Executor subagent × N（并行，全新上下文）
  └─ Verifier / Debug subagent（全新上下文）
```

每个角色获得独立的全新上下文窗口，避免上下文腐烂。

## 支持的运行时（15+）

Claude Code、OpenCode、Gemini CLI、Kilo、Codex、Copilot、Cursor、Windsurf 等。

安装时自动检测运行时并配置对应目录（如 `~/.claude/skills/gsd-*/`）。

## 配置

配置文件：`.planning/config.json`

| 设置 | 作用 |
|------|------|
| `mode` | `interactive`（逐步确认）或 `yolo`（自动批准） |
| 模型配置 | `quality` / `balanced` / `budget` 控制每个 agent 使用的模型 |
| `workflow.research` / `plan_check` / `verifier` | 开关质量 agent（增加 token 和时间） |
| `parallelization.enabled` | 并行运行独立计划 |

## 与其他工具的对比

| 工具 | 定位 | GSD 的差异 |
|------|------|-----------|
| [[addyosmani-agent-skills]] | 22 个开发生命周期技能 | GSD 是完整项目管理框架，不只是单个技能 |
| [[superpowers]] | 软件开发方法论编码 | GSD 更轻量，聚焦 Spec→Ship 全流程 |
| [[karpathy-inspired-claude-code-guidelines]] | Claude Code 行为准则 | GSD 包含上下文工程和多 Agent 编排 |
| [[andrej-karpathy-skills]] | Karpathy 风格的技能包 | GSD 有完整的项目状态管理和里程碑系统 |

## 适用场景

- 独立开发者用 AI 编程构建完整项目
- 需要结构化工作流但不想管理 Jira/sprint 的团队
- 长周期项目需要跨会话保持上下文一致性

## 局限性

- 深度绑定 Claude Code 生态（虽支持其他运行时，Claude Code 体验最佳）
- 61k stars 但有 $GSD Token（加密货币关联，需注意风险）
- `yolo` 模式下完全跳过人工确认，适合小项目但大项目需谨慎

## 相关页面

- [[harness-engineering]] — GSD 是 Harness Engineering 的实践案例
- [[addyosmani-agent-skills]] — 同类 AI 编程技能系统
- [[karpathy-inspired-claude-code-guidelines]] — GSD 内含类似的行为约束
- [[claude-code-skills]] — GSD 属于 Claude Code 技能生态
