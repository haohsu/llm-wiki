---
title: 知识即代码 (Knowledge-as-Code)
created: 2026-04-13
updated: 2026-04-13
type: concept
tags: [agent, trend, open-source]
sources: [raw/articles/即刻-ai-agent-markdown-tools-2026-04-13.md]
---

# 知识即代码 (Knowledge-as-Code)

2026 年兴起的一个趋势：各领域专业人士将自己的领域知识结构化为 Markdown 文件，供 AI Agent 消费和执行。

## 核心理念

> "以前觉得'让 AI 变聪明'是模型公司的事，现在发现每个人都能做。把自己领域的专业知识结构化，写成一个 .md 文件，丢进去，Agent 就懂了。"

这种模式将专业知识从人的隐性知识转化为机器可读的显性指令，相当于给 Agent 装上了特定领域的"大脑"。

## 主要方向

| 方向 | 代表项目 | 说明 |
|------|----------|------|
| Agent 指令标准 | [[agents.md]], [[llms-txt]] | 统一格式让 Agent 理解项目/网站 |
| 设计系统 | [[awesome-design-md]] | 55+ 大厂设计规范 Markdown 化 |
| 前端风格控制 | [[taste-skill]] | 可调节的设计参数旋钮 |
| 软件开发方法论 | [[superpowers]] | 编码为 Agent 必须执行的工作流 |
| 多角色协作 | [[gstack]], [[agency-agents]] | 认知角色模板，覆盖多个职能部门 |
| 职业技能模块 | [[product-manager-skills]], [[aicmo-marketing]] | PM、营销等领域的技能包 |
| 代码教育 | [[codebase-to-course]] | 代码仓库转交互式教程 |

## 为什么重要

- **民主化 AI 增强**：不再依赖模型公司，个人就能让 Agent 变聪明
- **跨职业同时发生**：开发、设计、PM、营销都在做类似的事
- **速度超出预期**：项目 star 数快速增长（[[superpowers]] 121k, [[agency-agents]] 52k）
- **可组合性**：不同领域的 .md 文件可以混搭使用

## 与 Hermes Agent 的关系

Hermes Agent 的 [[claude-code-skills]] 生态本质上也是这个趋势的一部分——用 Markdown/YAML 文件定义 Agent 的行为和知识。区别在于 Hermes 更侧重工作流编排（触发条件、步骤、验证），而上述项目更侧重领域知识的结构化表达。

## 开放问题

- 这些 .md 标准最终会收敛为少数几个，还是持续分化？
- 当 Agent 能力增强后，外部 .md 知识文件的必要性是否会降低？
- 不同格式之间的互操作性如何保证？
