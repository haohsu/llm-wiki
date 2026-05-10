---
title: UI UX Pro Max
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, agent, tool, product, design]
sources: [https://github.com/nextlevelbuilder/ui-ux-pro-max-skill]
---

# UI UX Pro Max (UUPM)

为 AI 编程 Agent 提供设计智能的技能包，跨 15 个技术栈生成专业级 UI/UX 设计系统。v2.0 核心特性：AI 驱动的设计系统生成器。

- GitHub: [github.com/nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)
- 官网: [uupm.cc](https://uupm.cc)
- npm: `uipro-cli`
- Stars: 76,106 | Forks: 7,845
- 语言: Python
- 创建: 2025-11-30
- 许可: MIT

## 核心数据

| 维度 | 数量 | 说明 |
|------|------|------|
| 推理规则 | 161 | 行业特定设计系统生成规则 |
| UI 风格 | 67 | 玻璃拟态、粘土拟态、极简、粗野主义等 |
| 配色方案 | 161 | 与 161 种产品类型 1:1 对齐 |
| 字体配对 | 57 | 含 Google Fonts 导入链接 |
| 图表类型 | 25 | 仪表盘和分析推荐 |
| 技术栈 | 15 | React/Next.js/Vue/Svelte/SwiftUI/Flutter 等 |
| UX 指南 | 99 | 最佳实践、反模式、无障碍规则 |

## v2.0 核心：设计系统生成器

AI 驱动的推理引擎，分析项目需求后秒级生成完整设计系统。

### 工作流程

```
用户请求 → 5 路并行搜索 → 推理引擎 → 完整设计系统输出
             ├─ 产品类型匹配（161 类）
             ├─ 风格推荐（67 种）
             ├─ 配色方案（161 种）
             ├─ 着陆页模式（24 种）
             └─ 字体配对（57 组）
```

### 输出示例（Serenity Spa）

```
模式: Hero-Centric + Social Proof（情感驱动 + 信任元素）
风格: Soft UI Evolution（柔和阴影、微妙深度、有机形状）
配色: #E8B4B8 (Soft Pink) / #A8D5BA (Sage Green) / #D4AF37 (Gold)
字体: Cormorant Garamond / Montserrat（优雅、沉静、精致）
效果: 柔和阴影 + 平滑过渡 200-300ms + 温和悬停状态
避免: 鲜艳霓虹色 + 刺眼动画 + 暗色模式 + AI 紫粉渐变
```

### 161 条行业推理规则

| 类别 | 示例行业 |
|------|----------|
| 科技/SaaS | SaaS、微 SaaS、B2B、开发者工具、AI 平台、网络安全 |
| 金融 | 金融科技/加密、银行、保险、个人理财、发票工具 |
| 医疗 | 诊所、药房、牙科、兽医、心理健康、用药提醒 |
| 电商 | 通用、奢侈品、P2P 市场、订阅盒、外卖 |
| 服务 | 美容/水疗、餐厅、酒店、法律、家政、预约 |
| 创意 | 作品集、代理、摄影、游戏、音乐流、图片/视频编辑 |
| 生活 | 习惯追踪、食谱、冥想、天气、日记、情绪追踪 |
| 新兴 | Web3/NFT、空间计算、量子计算、自主无人机 |

每条规则包含：推荐模式、风格优先级、配色情绪、字体情绪、关键效果、反模式。

## 67 种 UI 风格（精选）

| 风格 | 最佳场景 |
|------|----------|
| 极简 & 瑞士风格 | 企业应用、仪表盘 |
| 玻璃拟态 | 现代 SaaS、金融仪表盘 |
| 粘土拟态 | 教育应用、儿童应用 |
| 粗野主义 | 设计作品集、艺术项目 |
| 暗色模式 (OLED) | 夜间模式、编码平台 |
| AI 原生 UI | AI 产品、聊天机器人、Copilot |
| Bento Grid | 产品功能、仪表盘 |
| 空间 UI (VisionOS) | VR/AR 应用 |
| 液态玻璃 | 高端 SaaS、奢侈品电商 |
| 低保真 / 原始美学 | 创意作品集 |

## 支持的 15 个技术栈

React、Next.js、Astro、Vue、Nuxt.js、Nuxt UI、Svelte、SwiftUI、React Native、Flutter、HTML+Tailwind、shadcn/ui、Jetpack Compose、Angular、Laravel

## 设计交付清单（内置）

UUPM 内置了预交付检查清单，Agent 生成代码时自动执行：

- [ ] 不用 emoji 做图标（用 SVG: Heroicons/Lucide）
- [ ] 所有可点击元素加 `cursor-pointer`
- [ ] 悬停状态 + 平滑过渡 150-300ms
- [ ] 亮色模式文字对比度 ≥ 4.5:1
- [ ] 键盘导航可见焦点状态
- [ ] 尊重 `prefers-reduced-motion`
- [ ] 响应式：375px / 768px / 1024px / 1440px

## 与同类工具的对比

| 维度 | UUPM | [[taste-skill]] | [[huashu-design]] |
|------|------|------|------|
| 定位 | 全栈设计智能系统 | 前端设计参数旋钮 | HTML 原型生成 |
| 风格数 | 67 种 | 3 个旋钮（冒险/动画/密度） | 单一风格 |
| 行业规则 | 161 条 | 无 | 无 |
| 技术栈 | 15 个 | 通用 | HTML |
| 适合场景 | 需要专业 UI/UX 的全栈项目 | 微调已有设计 | 快速原型 |

## 适用场景

- AI 编程 Agent 生成专业级 UI（不靠 Agent 自由发挥）
- 需要行业特定设计系统的项目
- 多平台（Web/iOS/Android）统一设计语言
- 非设计师也能获得专业设计输出

## 局限性

- 76k stars 但有 PayPal 捐赠链接（商业化倾向）
- 规则库固定，新行业/风格需等待更新
- 生成结果需人工审核，不适合直接用于生产
- Python 依赖，需运行 CLI 工具

## 实战组合技巧

> **ui-ux-pro-max + baoyu-markdown-to-html** = 可视化 HTML 输出
> 
> 先用 UUPM 设计系统生成器确定风格/配色/字体，再用 `baoyu-markdown-to-html` 将 Markdown 转为带设计系统的 HTML。Agent 同时加载两个技能即可实现一站式内容→可视化页面。

## 相关页面

- [[taste-skill]] — 同类前端设计辅助，但更轻量（3 个旋钮）
- [[huashu-design]] — 另一种 HTML 设计生成工具
- [[addyosmani-agent-skills]] — 同类 Agent 技能包（侧重开发流程）
- [[awesome-design-md]] — 大厂设计规范 Markdown 集合
- [[baoyu-skills]] — 与 baoyu-markdown-to-html 配合生成可视化 HTML
- [[claude-code-skills]] — UUPM 属于 Claude Code 技能生态
