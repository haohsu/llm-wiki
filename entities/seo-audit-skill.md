---
title: JeffLi1993/seo-audit-skill
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, tool, agent, product]
sources: [https://github.com/JeffLi1993/seo-audit-skill]
---

# SEO Audit Skill

可复用的单页面 SEO 审计 Agent Skill。给一个 URL，输出结构化 HTML 审计报告，包含可执行的修复建议。

- GitHub: [github.com/JeffLi1993/seo-audit-skill](https://github.com/JeffLi1993/seo-audit-skill)
- 作者: Jeff (JeffLi1993)
- 许可: MIT
- 定位: Agent 原生的 SEO 审计工具
- 背景: Powered by OpenClaw

## 核心架构：Script + LLM 双层设计

```
URL → Layer 1: Python 脚本（确定性检查 → JSON）
        ↓ JSON + llm_review_required 标志
      Layer 2: LLM Agent（仅语义判断）
        ↓
      report-template.html → reports/<hostname>-audit.html
```

**为什么分两层？**
- 脚本处理 80% 确定性检查（robots.txt 是否存在？Title 是否 55 字符？）
- LLM 处理 20% 需要理解力的判断（H1 是否语义覆盖搜索意图？）
- `llm_review_required` 标志确保 LLM 仅在脚本无法判断时才介入
- 事实性检查无幻觉，语义性检查无盲区

## 两个 Skill

| Skill | 层级 | 适用场景 |
|-------|------|----------|
| seo-audit | Basic | 默认入口 — 给 URL，输出结构化首轮检查 |
| seo-audit-full | Full | 深度审计：Core Web Vitals、内容质量、GSC、竞品差距 |

## 审计覆盖范围（20+ 检查项）

### 站点级

| 检查项 | 检查内容 | Basic | Full |
|--------|----------|:---:|:---:|
| robots.txt | RFC 9309 指令组解析、Allow/Disallow、Googlebot 状态 | ✅ | ✅ |
| sitemap.xml | 有效 XML、URL 数量、追踪 robots.txt 的 Sitemap 路径 | ✅ | ✅ |
| 404 处理 | 真 404 vs 软 404 vs 跳转首页 | ✅ | ✅ |
| URL 规范化 | HTTP→HTTPS、www 一致性、尾斜杠、Canonical 标签 | ✅ | ✅ |
| i18n / hreflang | 互相引用对称、BCP 47、x-default | ✅ | ✅ |
| Schema (JSON-LD) | @type 检测、必填字段、@graph 展平、类型冲突 | ✅ | ✅ |
| E-E-A-T 信任页面 | About/Contact/Privacy/Terries 存在 + footer/nav 可达 | ✅ | ✅ |
| GSC 抓取状态 | 索引覆盖、抓取错误 | — | ✅ |
| Core Web Vitals | CrUX 字段数据：LCP、CLS、INP | — | ✅ |

### 页面级

| 检查项 | 检查内容 | Basic | Full |
|--------|----------|:---:|:---:|
| URL Slug | 小写、连字符、含关键词、停用词/堆砌检测 | ✅ | ✅ |
| Title | 50–60 字符、关键词位置、首页 vs 内页规则 | ✅ | ✅ |
| Meta Description | 120–160 字符、关键词匹配、具体价值主张 | ✅ | ✅ |
| H1 标签 | 唯一 H1、关键词匹配（full/partial/none） | ✅ | ✅ |
| Canonical 标签 | 自引用、与重定向后最终 URL 一致 | ✅ | ✅ |
| 图片 Alt 文本 | 所有 `<img>` 的 alt 属性检查 | ✅ | ✅ |
| 字数统计 | 正文 ≥ 500 词、薄内容标记 | ✅ | ✅ |
| 关键词位置 | 主关键词出现在正文前 100 词内 | ✅ | ✅ |
| 标题层级结构 | H2 数量（5–7）、H3/H2 比例、关键词分布 | ✅ | ✅ |
| 内部链接 | 同源链接数、权重分配 | ✅ | ✅ |
| OG / 社交标签 | og:image、twitter:card | — | ✅ |
| 内容质量 | E-E-A-T 深度、可读性、竞品对比 | — | ✅ |
| Robots Meta | noindex、nofollow、max-snippet | — | ✅ |

## 报告产出

每次审计生成独立 HTML 报告：

| 章节 | 内容 |
|------|------|
| Audit Summary | 一句话总结 + 关键问题/警告/通过项 |
| Site Checks | 可抓取性 · URL 规范化 · i18n · Schema · E-E-A-T |
| Page Checks | TDK · H1 · 标题层级 · 字数 · 内链 |
| Priority Actions | 影响最大的 3 项修复，按优先级排序 |
| Insight Walkthrough | Evidence → Impact → Fix |

## 内置脚本

| 脚本 | 功能 |
|------|------|
| check-site.py | robots.txt + sitemap — RFC 9309 指令组解析 |
| check-page.py | H1 / title / meta / canonical / URL slug — 停用词感知关键词匹配 |
| check-schema.py | JSON-LD 提取、@graph 展平、@type + 必填字段校验 |
| fetch-page.py | 原始 HTML 抓取 — SSRF 防护、重定向链追踪 |
| check-social.py | OG + Twitter Card 校验（仅 Full 版本） |

依赖：`pip install requests`

## 安装

```bash
# CLI 安装（推荐）
npx skills add JeffLi1993/seo-audit-skill

# 安装指定 Skill
npx skills add JeffLi1993/seo-audit-skill --skill seo-audit
npx skills add JeffLi1993/seo-audit-skill --skill seo-audit-full

# Claude Code Plugin
/plugin marketplace add JeffLi1993/seo-audit-skill
/plugin install seo-audit-skill
```

## 使用

```
audit this page: https://example.com
deep audit: https://example.com
```

## 方法论关系

- Script + LLM 双层架构与 [[video-use]] 的音频层+视觉层思路一致——用结构化中间表示替代原始数据
- 与 [[tavily-ai-skills]] 互补——Tavily 偏信息获取，seo-audit-skill 偏页面诊断
- 属于 [[claude-code-skills]] 生态中的 SEO 垂直领域技能
