# Wiki Log

> Chronological record of all wiki actions. Append-only.
> Format: `## [YYYY-MM-DD] action | subject`
> Actions: ingest, update, query, lint, create, archive, delete
> When this file exceeds 500 entries, rotate: rename to log-YYYY.md, start fresh.

## [2026-04-12] create | Wiki initialized
- Domain: Personal knowledge base and startup intelligence
- Structure created with SCHEMA.md, index.md, log.md
- GitHub repo: https://github.com/haohsu/llm-wiki

## [2026-04-12] ingest | baoyu-skills (github.com/JimLiu/baoyu-skills)
- Source: GitHub README (52KB)
- Raw saved: raw/articles/baoyu-skills-readme-2026-04-12.md
- Created:
  - entities/jim-liu.md — Jim Liu (宝玉) 人物页
  - entities/baoyu-skills.md — 项目概况（21 个技能，3 大类）
  - concepts/claude-code-skills.md — Claude Code 技能生态分析
  - concepts/ai-image-generation.md — 9 大 AI 图像 provider 对比
- Cross-references: 4 pages interlinked

## [2026-04-13] ingest | 即刻 - AI Agent Markdown 工具集合
- Source: https://web.okjike.com/u/695ACB1F-CBA8-4896-B105-4FE7981E4300/post/69da0f4a0cdc22382e37831b
- Raw saved: raw/articles/即刻-ai-agent-markdown-tools-2026-04-13.md
- Created concepts:
  - concepts/knowledge-as-code.md — 知识即代码趋势总览
  - concepts/agent-instruction-standards.md — agents.md 与 llms.txt 标准对比
- Created entities:
  - entities/agents-md.md — 通用 Agent 指令格式标准
  - entities/llms-txt.md — 网站对 LLM 可读标准
  - entities/awesome-design-md.md — 55+ 大厂设计规范集合 (4.3k ⭐)
  - entities/taste-skill.md — 前端设计参数旋钮 (7k+ ⭐)
  - entities/superpowers.md — 软件开发方法论编码为 Agent 工作流 (121k ⭐)
  - entities/gstack.md — YC CEO 的 Agent 多角色认知配置
  - entities/agency-agents.md — 147 职业角色模板 (52k+ ⭐)
  - entities/product-manager-skills.md — 46 个 PM 技能模块
  - entities/aicmo-marketing.md — 营销/运营 prompt 集合
  - entities/codebase-to-course.md — 代码仓库转交互式教程
- Cross-references: 12 pages interlinked via [[wikilinks]]
- Total wiki pages: 16 (was 4)

## [2026-04-13] create | AI + 知识图谱驱动项目创新方案
- Created: concepts/ai-knowledge-graph-project-innovation.md
- Content: GitNexus 知识图谱 + LLM 的 7 个创新应用场景 + 落地路线图
- Updated: index.md (新增 1 条目，total 5)

## [2026-04-13] update | AI + 知识图谱驱动项目创新方案
- 修改: concepts/ai-knowledge-graph-project-innovation.md
- 内容: 移除项目耦合，改为通用方案（基础设施前提、行业专项场景通用模板、路线图泛化）

## [2026-04-13] query | GitNexus vs TreeSitter+Neo4j 方案对比
- Session: gitnexuswithai
- 内容: 两种代码知识图谱方案的架构、优劣、选型建议
- 结论: GitNexus 适合快速启动，TreeSitter+Neo4j 适合深度定制，可混合使用

## [2026-04-14] ingest | andrej-karpathy-skills (github.com/forrestchang/andrej-karpathy-skills)
- Source: GitHub README (5741 chars)
- Raw saved: raw/articles/andrej-karpathy-skills-readme-2026-04-14.md
- Created:
  - entities/andrej-karpathy-skills.md — 项目概述（基于 Karpathy 观察的 Claude Code 指南）
  - concepts/karpathy-inspired-claude-code-guidelines.md — 四大原则详细分析
- Updated:
  - concepts/claude-code-skills.md — 添加竞品引用和相关页面链接
  - index.md — 新增 2 条目，total 7
- Cross-references: 4 pages interlinked

## [2026-04-14] lint | Wiki 健康检查
- 检查时间: 2026-04-14 10:55
- 总页面数: 20
- 发现问题: 14 个
- 主要问题:
  1. 孤立页面 (3): README, agents-md, ai-knowledge-graph-project-innovation
  2. 断开链接 (3): 三个页面链接到不存在的 "agents.md"
  3. 索引不完整: README 不在索引中，总页面数错误 (报告7，实际20)
  4. Frontmatter 问题 (4): README 缺少 frontmatter，三个页面使用无效标签 'standard'
  5. 页面过大: ai-knowledge-graph-project-innovation 有206行
- 建议修复:
  1. 为孤立页面添加入站链接或考虑归档
  2. 修复断开的链接：将 "agents.md" 改为 "agents-md"
  3. 更新 index.md：添加 README 条目，修正总页面数为 20
  4. 修复 frontmatter：为 README 添加 frontmatter，将 'standard' 标签添加到 SCHEMA.md 或替换为有效标签
  5. 拆分过大的页面：ai-knowledge-graph-project-innovation 考虑拆分为子主题

## [2026-04-14] lint-fix | 修复 Wiki 健康问题
- 修复时间: 2026-04-14 11:00
- 修复的问题:
  1. 断开的链接: 将 knowledge-as-code.md、llms-txt.md、superpowers.md 中的 [[agents.md]] 替换为 [[agents-md]]
  2. 无效标签: 将 agents-md.md、llms-txt.md 中的 'standard' 标签替换为 'tool'
  3. 索引总页面数: 更新 index.md 中的总页面数从 7 为 20
  4. 孤立页面: 在 claude-code-skills.md 中添加对 ai-knowledge-graph-project-innovation 的引用
- 剩余问题:
  1. 页面过大: ai-knowledge-graph-project-innovation 有 205 行，建议拆分为子主题
  2. README.md 不是 wiki 页面，可考虑从孤立页面检查中排除

## [2026-04-14] ingest | Harness Engineering 文章集（20篇）
- Source: /mnt/d/xuhao/vault/AIHarness/raw/（20 篇文章）
- 主题: Harness Engineering — 围绕 AI Agent 设计约束、反馈、文档、生命周期管理的工程范式
- Created entities:
  - entities/openai-harness-engineering.md — OpenAI 百万行代码实验（零行手写，5个月，~1500 PR）
  - entities/anthropic-agent-harness.md — Anthropic 长时运行 Agent + 上下文工程 + 多 Agent 研究 + 并行编译器
  - entities/langchain-agent-harness.md — LangChain Agent=Model+Harness 公式，Top30→Top5 实验
  - entities/martin-fowler-harness-engineering.md — Thoughtworks 权威评析，Feedforward+Feedback 模型
  - entities/phil-schmid-agent-harness.md — Phil Schmid 2026年1月预言 Agent Harness 定义全年
- Created concepts:
  - concepts/harness-engineering.md — 核心概念：定义、时间线、工程师角色转变、实验数据
  - concepts/harness-engineering-components.md — 四大支柱：分层上下文、Agent 专业化、持久记忆、背压
  - concepts/harness-engineering-vs-context-engineering.md — Prompt/Context/Harness 三层辨析
  - concepts/agent-harness-patterns.md — 实践模式：长时运行、多 Agent、五大战术组件
- Cross-references: 9 pages interlinked via [[wikilinks]]
- Total wiki pages: 27 (was 20)

## [2026-04-14] ingest | multica (github.com/multica-ai/multica)
- Source: GitHub README (11.5k stars, Go + TypeScript)
- Raw saved: raw/articles/multica-readme-2026-04-14.md
- Created:
  - entities/multica.md — 开源 managed agents 平台，Agent 作为团队成员管理
- Cross-references: 1 page linked to harness-engineering, agent-harness-patterns, claude-code-skills
- Total wiki pages: 28 (was 27)
## [2026-05-01] ingest | 即刻 GitHub 每日趋势 2026-05-01
- Source: https://web.okjike.com/u/A9E2F644-A9EE-4E6C-B83B-6A0EFF4861A4/post/69f41064af7695b4cf9c5972
- Raw saved: raw/articles/jike-github-trending-2026-05-01.md
- Updated:
  - entities/superpowers.md — star 数 121k → 174k，添加新来源
- Created entities:
  - entities/warp.md — 终端智能开发环境 (49k ⭐)
  - entities/trading-agents.md — 多智能体 LLM 金融交易框架 (57k ⭐)
  - entities/mattpocock-skills.md — 工程技能工具集 (49k ⭐)
  - entities/craft-agents-oss.md — Agent 协作工具 (5.5k ⭐)
  - entities/public-apis.md — 免费公共 API 集合 (429k ⭐)
  - entities/jcode.md — 高性能编码代理 (1.9k ⭐)
  - entities/maigret.md — OSINT 用户名搜索工具 (20k ⭐)
  - entities/ghost-track.md — OSINT 追踪工具 (12k ⭐)
  - entities/quarkdown.md — Markdown 排版系统 (13k ⭐)
- Total wiki pages: 37 (was 28)
