---
title: mattpocock/skills
created: 2026-05-01
updated: 2026-05-01
type: entity
tags: [tool, agent, open-source]
sources: [raw/articles/jike-github-trending-2026-05-01.md, raw/articles/mattpocock-skills-readme-2026-05-01.md]
---

# mattpocock/skills

- **GitHub**: https://github.com/mattpocock/skills
- **Stars**: 49,663
- **作者**: Matt Pocock（Total TypeScript 创始人，知名 TypeScript 教育者）
- **定位**: 面向"真正的工程师"的 Agent 技能集合，修复编码 Agent 的常见失败模式

## 核心理念

与 [[superpowers]] 等"编码整套方法论"不同，skills 采用**小而可组合**的设计哲学——每个技能解决一个具体的工程问题，不控制整个流程。作者明确反对 "vibe coding"，强调软件工程基本功在 AI 时代更重要。

## 解决的四大失败模式

### 1. Agent 没有做你想要的事（对齐问题）

最常见的失败模式：你以为 Agent 理解了需求，结果它做出来的东西完全不对。

- `/grill-me` — 非代码场景的"拷问"会话，Agent 会详细追问你到底要什么
- `/grill-with-docs` — 代码场景，结合领域模型挑战你的计划，同时更新 `CONTEXT.md` 和 ADR

这是最受欢迎的技能，每次动手前都应该用。

### 2. Agent 太啰嗦（语言问题）

Agent 刚进入项目时不懂领域术语，用 20 个词表达 1 个词就能说清的事。

**解法：共享语言** — `CONTEXT.md` 文件定义项目的领域术语。效果：
- 变量、函数、文件命名一致
- Agent 导航代码更快
- Agent 思考消耗更少 token

`/grill-with-docs` 会自动帮你建立共享语言。

### 3. 代码不能用（反馈问题）

Agent 没有代码如何运行的反馈，就会"盲飞"。

**解法：反馈循环** — 静态类型、浏览器访问、自动化测试。

- `/tdd` — 红-绿-重构循环，先写失败测试再修复
- `/diagnose` — 纪律性诊断循环：复现 → 最小化 → 假设 → 插桩 → 修复 → 回归测试

### 4. 建出了一坨泥球（设计问题）

Agent 加速编码的同时也加速了软件熵增，代码库变得复杂难改。

- `/zoom-out` — 让 Agent 在系统全局上下文中解释代码
- `/improve-codebase-architecture` — 发现代码库中的"深化"机会，建议每隔几天运行一次

## 技能清单（15 个）

### Engineering（9 个）

| 技能 | 说明 |
|------|------|
| `/diagnose` | 纪律性 bug 诊断循环 |
| `/grill-with-docs` | 拷问会话 + 领域文档 + ADR |
| `/triage` | 通过状态机分流 issues |
| `/improve-codebase-architecture` | 代码库架构改善 |
| `/setup-matt-pocock-skills` | 一次性项目配置（issue tracker、标签、文档目录） |
| `/tdd` | 红-绿-重构测试驱动开发 |
| `/to-issues` | 将计划/PRD 拆分为独立 GitHub issues（垂直切片） |
| `/to-prd` | 将对话上下文转为 PRD 并提交为 GitHub issue |
| `/zoom-out` | 让 Agent 从更高视角解释代码 |

### Productivity（3 个）

| 技能 | 说明 |
|------|------|
| `/caveman` | 超压缩通信模式，减少 75% token 消耗 |
| `/grill-me` | 非代码场景的深度访谈 |
| `/write-a-skill` | 创建新技能（结构、渐进披露、资源打包） |

### Misc（3 个）

| 技能 | 说明 |
|------|------|
| `/git-guardrails-claude-code` | Claude Code hooks 阻止危险 git 命令 |
| `/migrate-to-shoehorn` | 迁移测试文件的类型断言 |
| `/scaffold-exercises` | 创建练习目录结构 |

## 安装方式

```bash
npx skills@latest add mattpocock/skills
```

交互式选择要安装的技能和目标 Agent，然后在 Agent 中运行 `/setup-matt-pocock-skills` 完成配置。

## 与生态的关系

- 与 [[superpowers]] 同属 Agent 技能方向，但哲学不同：superpowers 编码整套方法论（强制性），skills 提供小工具（可选组合）
- 与 [[baoyu-skills]] 都是 Claude Code 技能集合，但 skills 更聚焦软件工程基本功
- 与 [[claude-code-skills]] 生态高度相关
- `/grill-with-docs` 的共享语言理念与 [[knowledge-as-code]] 趋势一致
- `/tdd` 与 [[andrej-karpathy-skills]] 中的测试优先原则呼应
