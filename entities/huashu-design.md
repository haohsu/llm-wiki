---
title: Huashu Design
created: 2026-05-01
updated: 2026-05-01
type: entity
tags: [tool, agent, open-source, product]
sources: [https://github.com/alchaincyf/huashu-design]
---

# Huashu Design（花束设计）

- **GitHub**: https://github.com/alchaincyf/huashu-design
- **Stars**: 10,897
- **作者**: alchaincyf
- **语言**: HTML
- **创建时间**: 2026-04-19
- **定位**: HTML 原生的 Agent 设计技能——一句话 prompt 出可交付的设计

> 「打字。回车。一份能交付的设计。」

## 核心能力

| 能力 | 交付物 | 典型耗时 |
|------|--------|----------|
| 交互原型（App / Web） | 单文件 HTML · 真 iPhone bezel · 可点击 · Playwright 验证 | 10–15 min |
| 演讲幻灯片 | HTML deck + 可编辑 PPTX（真文本框） | 15–25 min |
| 时间轴动画 | MP4（25fps/60fps 插帧）+ GIF + BGM | 8–12 min |
| 设计变体 | 3+ 并排对比 · Tweaks 实时调参 | 10 min |
| 信息图 / 可视化 | 印刷级排版 · 可导 PDF/PNG/SVG | 10 min |
| 设计方向顾问 | 5 流派 × 20 种设计哲学 · 推荐 3 方向 · 并行生成 Demo | 5 min |
| 5 维度专家评审 | 雷达图 + Keep/Fix/Quick Wins 清单 | 3 min |

## 核心机制

### 品牌资产协议（5 步硬流程）

涉及具体品牌时强制执行，这是 skill 里最硬的一段规则：

1. **问** — 用户有 brand guidelines 吗？
2. **搜官方品牌页** — `<brand>.com/brand` · `brand.<brand>.com` · `<brand>.com/press`
3. **下载资产** — SVG → 官网 HTML → 产品截图取色（三条兜底）
4. **grep 提取色值** — 从资产里抓所有 `#xxxxxx`，按频率排序，过滤黑白灰。**绝不从记忆猜品牌色**
5. **固化 spec** — 写 `brand-spec.md` + CSS 变量，所有 HTML 引用 `var(--brand-*)`

A/B 测试：v2 稳定性方差比 v1 低 5 倍。

### 设计方向顾问（Fallback）

需求模糊时触发：从 5 流派 × 20 种设计哲学推荐 3 个**必须来自不同流派**的方向，每个配代表作、气质关键词、代表设计师，并行生成 3 个视觉 Demo 让用户选。

### Junior Designer 工作流

不闷头做大招：先写 assumptions + placeholders + reasoning，尽早 show 给用户，再迭代。理解错了早改比晚改便宜 100 倍。

## 安装方式

```bash
npx skills add alchaincyf/huashu-design
```

Agent 通用——Claude Code、Cursor、Codex、OpenClaw、Hermes 都能装。

## 与生态的关系

- 属于 [[claude-code-skills]] 生态中最具视觉冲击力的设计技能
- 与 [[baoyu-skills]] 互补：baoyu-skills 做内容生成+多平台发布，huashu-design 做视觉设计+原型
- 与 [[mattpocock-skills]] 同属 `skills.sh` 生态，但聚焦设计而非工程
- 与 [[taste-skill]] 方向相近：taste-skill 提供设计参数旋钮，huashu-design 提供完整设计交付能力
- 与 [[awesome-design-md]] 理念一致：把设计规范编码为机器可读的形式
- HTML 原生输出体现了 [[knowledge-as-code]] 趋势——用代码（HTML/CSS）而非设计工具承载设计
- 品牌资产协议的"绝不从记忆猜品牌色"原则，是 Agent 可靠性工程的典范
