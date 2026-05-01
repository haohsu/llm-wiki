---
title: Superpowers
created: 2026-04-13
updated: 2026-05-01
type: entity
tags: [agent, tool, open-source]
sources: [raw/articles/即刻-ai-agent-markdown-tools-2026-04-13.md, raw/articles/jike-github-trending-2026-05-01.md]
---

# Superpowers

- **GitHub**: https://github.com/obra/superpowers
- **Stars**: 174k（[[knowledge-as-code]] 领域最多）
- **作者**: obra
- **定位**: 完整的软件开发方法论，编码为 Agent 必须执行的工作流

## 核心特性

- 用 Markdown 编码整套开发方法论
- Agent 如果写代码之前没写测试，代码会被自动删掉
- 涵盖设计评审、分支管理、代码审查
- 每个环节都有对应的 skill 文件

## 激进的设计理念

与 [[agents-md]] 的"建议性"指令不同，Superpowers 是**强制性**的——Agent 必须遵循预定义的工作流，否则产出会被拒绝。这相当于把人类的 best practices 变成了机器可执行的约束。

## 与生态的关系

- 比 [[agent-instruction-standards]] 更进一步：不只是让 Agent 理解项目，而是控制 Agent 的行为
- 与 [[gstack]] 互补：Superpowers 强调方法论执行，GStack 强调多角色认知切换
- 与 [[claude-code-skills]] 理念相似，但更聚焦于软件开发全流程
