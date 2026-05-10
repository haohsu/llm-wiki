---
title: tavily-ai/skills
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, tool, api, agent, product]
sources: [https://github.com/tavily-ai/skills]
---

# Tavily Agent Skills

Tavily 官方的 Agent 技能集合，为 Claude Code、Cursor 等 AI 编程助手提供 LLM 优化的 Web 搜索、内容提取、站点爬取、URL 发现和深度研究能力。

- GitHub: [github.com/tavily-ai/skills](https://github.com/tavily-ai/skills)
- 版本: 0.1.1
- 语言: Python（≥3.10）
- 许可: MIT
- 依赖: tavily-python, click, rich, httpx
- 定位: Agent 原生的 Web 搜索工具链

## 核心理念

**用结构化中间表示替代原始数据**，大幅降低 token 消耗，提升推理质量。

传统方式：直接返回原始网页 → 上下文被导航栏、Cookie 横幅、样板代码淹没
Tavily 方式：返回 LLM 优化的结构化 JSON → 只有精炼信息进入上下文

与 [[video-use]] 的方法论一脉相承：用结构化中间表示替代原始数据。

## 8 个技能

| 技能 | 用途 | 命令 |
|------|------|------|
| tavily-search | Web 搜索，返回 LLM 优化结果 | `tvly search "query" --json` |
| tavily-extract | 从 URL 提取干净 Markdown | `tvly extract "url" --json` |
| tavily-crawl | 爬取站点，批量提取多页内容 | `tvly crawl "url" --output-dir ./docs/` |
| tavily-map | 发现站点所有 URL（不提取内容） | `tvly map "url" --json` |
| tavily-research | AI 驱动深度研究，多源综合+引用 | `tvly research "topic" --model pro` |
| tavily-dynamic-search | 程序化搜索，防止上下文污染 | Python heredoc 模式 |
| tavily-cli | 总览技能，安装/认证指南 | `tvly --help` |
| tavily-best-practices | 生产级集成参考文档 | — |

## 工作流：逐级升级

```
Search → Extract → Map → Crawl → Research
  ↑        ↑        ↑       ↑         ↑
 找页面   取内容   发现URL  批量提取   深度研究
```

原则：从简单开始，按需升级。

## Search 深度

| 深度 | 速度 | 精准度 | 适用场景 |
|------|------|--------|----------|
| ultra-fast | 最快 | 较低 | 实时聊天、自动补全 |
| fast | 快 | 良好 | 需要 chunks，延迟敏感 |
| basic | 中等 | 高 | 通用（默认） |
| advanced | 较慢 | 最高 | 精确事实查找 |

## Research 模型

| 模型 | 用途 | 速度 |
|------|------|------|
| mini | 单主题定向研究 | ~30s |
| pro | 多角度综合分析 | ~60-120s |
| auto | API 自动选择 | 不定 |

## Dynamic Search：防止上下文污染

核心思想：**程序化工具调用（PTC）**，复用 Anthropic 的架构理念。

```
tvly search "query" --json | python3 -c "import json,sys; ..."
```

- 搜索结果（~300K 字符）留在 Python 进程内存中
- 只有 `print()` 输出进入 LLM 上下文（~1-3K 字符）
- **100-200x 上下文压缩**

支持多轮迭代：Turn 1 搜索+分诊 → Turn 2 定向提取 → Turn 3 深入细节。
数据持久化到 `/tmp/` 文件，上下文保持精简。

## 安装

```bash
# 安装技能
npx skills add https://github.com/tavily-ai/skills

# 安装 CLI
curl -fsSL https://cli.tavily.com/install.sh | bash

# 认证
tvly login --api-key tvly-YOUR_KEY
# 或: export TAVILY_API_KEY=tvly-...
```

## 与 Hermes 的关系

Tavily 技能遵循 `npx skills add` 安装标准（与 [[baoyu-skills]]、[[mattpocock-skills]] 等同类），但其核心价值在于 **Agent 原生的 Web 搜索工具链**，可作为 Hermes web_search 工具的高级替代方案。

## 生态关系

- 属于 [[claude-code-skills]] 生态中的搜索/研究类技能
- 与 [[baoyu-skills]] 互补——baoyu 偏内容生成，Tavily 偏信息获取
- 方法论与 [[video-use]] 相同：用结构化中间表示替代原始数据
