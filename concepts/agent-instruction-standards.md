---
title: Agent 指令标准 (agents.md & llms.txt)
created: 2026-04-13
updated: 2026-04-13
type: concept
tags: [agent, standard, tool]
sources: [raw/articles/即刻-ai-agent-markdown-tools-2026-04-13.md]
---

# Agent 指令标准

两个互补的标准，分别解决 Agent 在项目级和网站级的理解问题。

## agents.md

- **官网**: https://agents.md/
- **定位**: 项目根目录的通用 Agent 指令格式
- **功能**: 放在项目根目录，所有主流 Agent（Claude Code、Cursor、Copilot 等）都可以读取并遵循
- **类比**: 相当于 `README.md` 给人看，`agents.md` 给 Agent 看

## llms.txt

- **目录站**: https://llmstxthub.com/
- **定位**: 让网站对 LLM 可读的标准
- **功能**: 放在网站根目录，用 Markdown 描述网站内容结构
- **类比**: `robots.txt` 给搜索引擎看，`llms.txt` 给大模型看
- **采用情况**: 已有 900+ 网站实现

## 两者的关系

| 维度 | agents.md | llms.txt |
|------|-----------|----------|
| 作用范围 | 项目/代码仓库 | 网站 |
| 目标受众 | 代码 Agent | 浏览/搜索 Agent |
| 放置位置 | 项目根目录 | 网站根目录 |
| 内容类型 | 开发规范、工作流指令 | 网站结构、内容摘要 |

两者都属于 [[knowledge-as-code]] 趋势的不同切面——用结构化 Markdown 让 AI Agent 更好地理解人类的项目和内容。

## 相关项目

- [[superpowers]] — 比 agents.md 更激进，直接编码整套开发方法论
- [[awesome-design-md]] — 设计系统的结构化表达，可配合 agents.md 使用
