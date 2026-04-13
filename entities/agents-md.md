---
title: agents.md
created: 2026-04-13
updated: 2026-04-13
type: entity
tags: [agent, standard]
sources: [raw/articles/即刻-ai-agent-markdown-tools-2026-04-13.md]
---

# agents.md

- **官网**: https://agents.md/
- **定位**: 项目根目录的通用 Agent 指令格式

## 核心特性

- 放在项目根目录的标准 Markdown 文件
- 所有主流 Agent（Claude Code、Cursor、Copilot 等）都可以读取
- 定义项目的开发规范、工作流、约束条件

## 与生态的关系

- `README.md` 给人看，`agents.md` 给 Agent 看
- 与 [[llms-txt]] 互补（项目级 vs 网站级）
- [[superpowers]] 比它更激进，直接编码整套方法论
- 属于 [[knowledge-as-code]] 趋势
