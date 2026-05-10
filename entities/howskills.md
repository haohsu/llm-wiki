---
title: howSkills
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, agent, tool, product]
sources: [https://mp.weixin.qq.com/s/qUqpiz2nzUi7c9VBuhUqMQ]
---

# /howSkills — Agent Skill 深度拆解命令

一条 Claude Code / Cursor 命令，自动深度拆解任意 Agent Skill，从产品视角提炼设计巧思和最佳实践。作者 comeonzhj（AI学习行动圈主理人）。

- GitHub: [comeonzhj/comeonzhj-claude-plugins](https://github.com/comeonzhj/comeonzhj-claude-plugins)
- 安装: `/plugin marketplace add comeonzhj/comeonzhj-claude-plugins` → `/plugin install ai-analyzer@comeonzhj-plugins`
- 适用: Claude Code、Cursor 等支持 commands 的 AI 编程工具
- 前作: `/howPrompt`（自动拆解开源项目工程实践）

## 八阶段分析流程

一条命令触发后，Agent 自动完成 8 个阶段的深度分析：

| 阶段 | 作用 |
|------|------|
| 结构扫描 | 识别 Skill 资源组成、类型分类 |
| 痛点挖掘 | 从实现细节反推真实用户痛点（不看文档自述） |
| 工作流可视化 | 自动生成时序图和流程图 |
| 脚本设计拆解 | 原子化程度、场景覆盖、接口设计 |
| 参考文档设计拆解 | 知识分层、渐进式披露策略 |
| 资产设计拆解 | 模板复用、品牌一致性 |
| 独特解法提炼 | 提炼可迁移的设计模式（最有价值部分） |
| 综合评估 | 5 维度打分 + 最佳实践总结 |

结果自动写入项目的 `analysis/howSkills.md`。

## 实战案例：拆解 hatch-pet（Codex 桌面宠物 Skill）

hatch-pet 是在 Codex 应用里创建动画桌面宠物的 Skill，运行一次消耗 Plus 账号 5 小时额度。

核心矛盾：**图像生成的不确定性 vs 精灵图的精确性要求**
- 一个宠物需要 10+ 次图像生成，每次保持同一角色形象
- 最终输出 1536×1872 精灵图集，每格 192×208，差一个像素就废
- 解法：15 个脚本 + 3 个参考文档 + 323 行指令，把创意任务变成确定性生产流水线

### 四个拍案设计

1. **身份锚点模式** — 首次生成后截取 `canonical-base.png` 作为视觉锚点，后续每次生成必须引用此图。把「一致性」从文字层面提升到视觉层面。

2. **色度键自适应** — 从参考图片采样像素，自动选距离最远的颜色当背景色。宠物是绿色？背景用品红色。避免固定绿色背景被宠物颜色干扰。

3. **镜像决策门控** — 不预设是否镜像，运行时决策。生成向右跑动画后，视觉检查有无不对称元素（蝴蝶结、文字），再决定镜像还是重新生成。省一半工作量。

4. **渐进式验证** — 每层都验证：录制时验证哈希、帧级别检查质量、图集级别检查几何精度。出问题立刻停在原地修复，不推倒重来。

## 五条可迁移最佳实践

| 模式 | 说明 | 适用场景 |
|------|------|----------|
| 身份锚点 | 多次生成任务中，视觉锚点比文字描述更可靠 | PPT、文档、任何多步生成 |
| 确定性-不确定性分离 | Agent 做创意决策，脚本做精确计算 | 任何需要精确输出的 Agent 任务 |
| 渐进式验证 | 每个关键节点设验证点，减少后期返工 | 长流程任务 |
| JSON 中间态 | 用文件做持久化状态，比上下文记忆更可靠 | 跨步骤状态管理 |
| 写边界隔离 | 子代理模式中明确「谁能写什么」 | 多 Agent 并行任务 |

## 设计理念

> Skills 是 Agent 生态里最值得研究的东西。一个好的 Skill，背后是一整套产品设计思维：怎么把模糊需求变成确定性流程？怎么管理 Agent 上下文窗口不溢出？怎么让脚本和提示词配合？怎么设计验证机制？

## 作者与社区

- 作者: comeonzhj（AI学习行动圈主理人）
- 社区: AI学习行动圈，5000+ 圈友，运营 700+ 天
- 平台: 8 个微信群 + 腾讯文档圈友空间 + 知识星球
- 前作: `/howPrompt`（拆解开源项目工程实践）

## 配置方式

**Claude Code / Cursor 直接复制：**
- 保存到 `~/.claude/commands/howSkills.md` 或项目根目录 `.claude/commands/howSkills.md`
- Cursor: `项目根目录/.cursor/commands/howSkills.md`

**Claude Code 插件安装：**
```
/plugin marketplace add comeonzhj/comeonzhj-claude-plugins
/plugin install ai-analyzer@comeonzhj-plugins
/ai-analyzer:howSkills
```

## 相关页面

- [[claude-code-skills]] — /howSkills 属于 Claude Code 技能生态
- [[knowledge-as-code]] — Skills 是知识结构化喂给 Agent 的实践
- [[karpathy-inspired-claude-code-guidelines]] — 同类 AI 编程最佳实践
- [[addyosmani-agent-skills]] — 另一个被拆解的典型 Skill 集合
