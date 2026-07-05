---
title: GSAP AI Skills
created: 2026-07-05
updated: 2026-07-05
type: entity
tags: [open-source, tool, skill, creative, design]
sources: [raw/articles/gsap-skills-README.md]
---

# GSAP AI Skills

GSAP (GreenSock Animation Platform) 官方 AI 技能包。教会 AI 编程 Agent 正确使用 GSAP 动画库：核心 API、时间线、ScrollTrigger、插件、React/Vue/Svelte 集成和性能优化。

- **GitHub**: https://github.com/greensock/gsap-skills
- **Stars**: 10,888 | **Forks**: 643
- **许可**: MIT
- **官网**: https://gsap.com
- **安装**: `npx skills add https://github.com/greensock/gsap-skills`

> 2026 年 Webflow 收购 GSAP 后，所有原 Club GSAP 插件（SplitText、MorphSVG 等）**全部免费**，包括商用。

## 8 个子技能

| 技能 | 内容 |
|------|------|
| **gsap-core** | 核心 API：`gsap.to()` / `from()` / `fromTo()`、easing、duration、stagger |
| **gsap-timeline** | 时间线：排序、position 参数、标签、嵌套、播放控制 |
| **gsap-scrolltrigger** | 滚动驱动动画：scroll-linked、pinning、scrub、refresh & cleanup |
| **gsap-plugins** | 插件：ScrollToPlugin、ScrollSmoother、Flip、Draggable、SplitText、ScrambleText、CustomEase 等 |
| **gsap-utils** | 工具函数：clamp、mapRange、normalize、interpolate、random、snap、wrap、pipe |
| **gsap-react** | React 集成：useGSAP hook、refs、`gsap.context()`、SSR、cleanup |
| **gsap-performance** | 性能优化：transform 优先于布局属性、will-change、batching |
| **gsap-frameworks** | Vue/Svelte 集成：生命周期、选择器作用域、卸载清理 |

## Agent Skills 格式

采用 [Agent Skills](https://agentskills.io) 标准格式，兼容 40+ AI 编程工具：

| Agent | 安装方式 |
|-------|---------|
| Claude Code | `npx skills add` 或 `/plugin marketplace add greensock/gsap-skills` |
| Cursor | `npx skills add` 或 Settings → Rules → Add Rule |
| Codex / Windsurf / Copilot | `npx skills add` |
| 其他 40+ | `npx skills add --agent <name>` |

## 标准 GSAP 模式

```javascript
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);

// 单次动画 — 优先 transform 别名和 autoAlpha
gsap.to(".box", { x: 100, autoAlpha: 1, duration: 0.6, ease: "power2.inOut" });

// 时间线 — 优先于链式 delay
const tl = gsap.timeline({ defaults: { duration: 0.5, ease: "power2" } });
tl.to(".a", { x: 100 }).to(".b", { y: 50 }, "+=0.2");

// ScrollTrigger — 挂到时间线或单次动画，布局变化后 refresh
gsap.timeline({ scrollTrigger: { trigger: ".section", start: "top center", scrub: true } })
  .to(".panel", { x: 100 });
```

## 风险等级

**LOW** — 纯动画库，安全面极小。

## 与同类技能包的对比

| 维度 | GSAP Skills | [[addyosmani-agent-skills]] | [[baoyu-skills]] |
|------|-------------|-----------------------------|-----------------|
| 定位 | 动画领域专家技能 | 软件工程全流程 | 内容生成+AI 工具链 |
| 子技能数 | 8 | 22 | 60+ |
| 领域 | 前端动画 | 工程实践 | 中国生态内容工具 |
| 特色 | GSAP 官方出品 | Google 工程文化 | 多平台发布 |
| 安装量 | 10k+ stars | 社区流行 | 14k+ stars |

## 适用场景

- AI 编程 Agent 生成 GSAP 动画代码（不靠幻觉）
- 需要 ScrollTrigger 滚动动画的项目
- React/Vue/Svelte 项目集成复杂动画
- 前端性能敏感型动画场景

## 相关页面

- [[addyosmani-agent-skills]] — 同类 Agent Skills 格式，含 frontend-ui-engineering 子技能
- [[baoyu-skills]] — 中文生态 AI 技能集合
- [[ui-ux-pro-max]] — UI/UX 设计系统技能，动画是其设计交付清单的一部分
- [[huashu-design]] — HTML 原型生成技能，含时间轴动画能力
- [[claude-code-skills]] — GSAP Skills 属于 Claude Code 技能生态
- [[excalidraw-diagram-generator]] — 同类 Agent Skills 格式的开源工具
