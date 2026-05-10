---
title: Flue
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, agent, architecture, product, platform]
sources: [https://github.com/withastro/flue]
---

# Flue — The Agent Harness Framework

Astro 团队（withastro）开源的 TypeScript Agent 框架，内置 Agent Harness。理念：像 Claude Code 一样构建 Agent，但 100% headless、可编程、无人值守。

状态：**Experimental**（API 可能变化）

- GitHub: [github.com/withastro/flue](https://github.com/withastro/flue)
- Stars: 2,990 | Forks: 154
- 语言: TypeScript
- 许可: MIT
- 创建: 2026-02-07
- 官网: [flueframework.com](https://flueframework.com)

## 核心定位

> "It's like Claude Code, but 100% headless and programmable."

Flue 不是又一个 AI SDK，而是一个运行时无关的 Agent 框架——类比 Astro 或 Next.js，但用于 Agent。写一次，构建，部署到任何地方（Node.js、Cloudflare、GitHub Actions、GitLab CI/CD）。

核心公式：**Agent = Model + Sandbox + Skills + Markdown**

## 架构

```
Flue Agent
├── Model（任意 LLM：Claude/GPT/Kimi 等）
├── Sandbox（执行环境）
│   ├── Virtual Sandbox（just-bash，轻量快速）
│   ├── Local（宿主文件系统，CI 场景）
│   └── Daytona Container（完整 Linux 环境）
├── Skills（Markdown 定义的技能）
├── AGENTS.md（Agent 行为指令）
└── Triggers（HTTP webhook / CLI / CI）
```

## 三种沙箱模式

| 模式 | 说明 | 适用场景 |
|------|------|----------|
| Virtual Sandbox | just-bash 驱动，内存文件系统 | 高流量 API Agent、轻量任务 |
| Local | 挂载宿主文件系统 `/workspace` | CI/CD、已 checkout 的仓库 |
| Daytona Container | 完整 Linux 容器（git/node/browser） | 编码 Agent、需要完整环境 |

## 包结构

| 包 | 说明 |
|---|------|
| `@flue/sdk` | 核心 SDK：构建系统、会话、工具 |
| `@flue/cli` | CLI：构建和运行 Agent |

## 四个示例场景

### 1. Hello World（最简 Agent）

```ts
export const triggers = { webhook: true };

export default async function ({ init, payload }: FlueContext) {
  const agent = await init({ model: 'anthropic/claude-sonnet-4-6' });
  const session = await agent.session();
  const result = await session.prompt(
    `Translate to ${payload.language}: "${payload.text}"`,
    { result: v.object({ translation: v.string(), confidence: v.picklist(['low','medium','high']) }) }
  );
  return result;
}
```

- Virtual Sandbox（默认），无需容器
- HTTP webhook 触发
- 结果 schema 验证（valibot）

### 2. Support Agent（R2 知识库）

```ts
const sandbox = await getVirtualSandbox(env.KNOWLEDGE_BASE); // R2 bucket
const agent = await init({ sandbox, model: 'openrouter/moonshotai/kimi-k2.6' });
```

- R2 bucket 挂载为 Agent 文件系统
- Agent 用内置工具（grep/glob/read）搜索知识库
- 消息历史自动持久化（Cloudflare Durable Objects）

### 3. Issue Triage（CI 触发）

```ts
const npm = defineCommand('npm');
const gh = defineCommand('gh', { env: { GH_TOKEN: process.env.GH_TOKEN } });

const agent = await init({ sandbox: 'local', model: 'anthropic/claude-opus-4-7' });
const result = await session.skill('triage', {
  args: { issueNumber: payload.issueNumber },
  commands: [gh, npm],
  result: v.object({ severity: v.picklist(['low','medium','high','critical']), ... }),
});
```

- CI 环境中运行，挂载宿主文件系统
- 特权 CLI（gh/npm）安全注入，Agent 看不到密钥
- Skill 引用：按 frontmatter `name:` 或路径

### 4. Coding Agent（Daytona 容器）

```ts
const client = new Daytona({ apiKey: env.DAYTONA_API_KEY });
const sandbox = await client.create();
const agent = await init({ sandbox: daytona(sandbox), model: 'openai/gpt-5.5' });
await setup.shell(`git clone ${payload.repo} /workspace/project`);
```

- 完整 Linux 容器，支持 git/node/browser
- 容器镜像声明式构建，首次构建后缓存
- 可在同一沙箱中启动多个 Agent 会话

## 关键设计决策

| 设计 | 说明 |
|------|------|
| Markdown 驱动 | Skills、Context、AGENTS.md 都是 Markdown，Agent 的"逻辑"在 Markdown 而非代码 |
| 无 TUI/GUI | 纯 TypeScript，无界面假设，适合 headless 部署 |
| Virtual Sandbox 默认 | just-bash 比容器快 10x+，适合高流量场景 |
| Schema 验证 | valibot schema 确保 Agent 返回类型安全的结果 |
| Connectors | 第三方服务适配器，用 Markdown 安装指令而非 npm 包 |
| 按需模型覆盖 | init/prompt/skill 每层都可覆盖 model，灵活控制成本 |

## CLI 命令

```bash
flue dev --target node          # 开发服务器（watch mode，端口 3583）
flue dev --target cloudflare    # Cloudflare Workers 开发服务器
flue run <agent> --target node  # 一次性运行（CI 场景）
flue build --target node        # 构建部署产物
flue build --target cloudflare  # 构建 Cloudflare Workers
flue add <connector> | claude   # 添加连接器（管道给 AI coding agent 处理）
```

## 与 [[harness-engineering]] 的关系

Flue 是 Harness Engineering 理念的框架级实现：
- **Agent = Model + Harness** — Flue 的 sandbox + skills + AGENTS.md 就是 Harness
- **工程师 = 骑手** — 用 TypeScript 定义 Agent 运行环境，而非写业务代码
- **Markdown 为王** — Skills 和指令在 Markdown 中，符合 [[knowledge-as-code]] 趋势

## 与同类工具的对比

| 维度 | Flue | [[get-shit-done]] | [[multica]] |
|------|------|------|------|
| 定位 | Agent Harness 框架 | Spec 驱动开发系统 | Managed Agents 平台 |
| 语言 | TypeScript | Markdown + Bash | TypeScript + Go |
| 部署 | Node.js / Cloudflare / CI | 本地 CLI | 自托管 / 云 |
| 沙箱 | Virtual / Local / Container | 无（Claude Code 原生） | 无（Agent 原生） |
| 适合场景 | 构建可编程 Agent 服务 | 个人 AI 编程项目管理 | 团队 Agent 协作 |

## 适用场景

- 构建可部署的 Agent 服务（客服/分诊/编码）
- CI/CD 中集成 AI Agent（GitHub Actions / GitLab CI）
- 需要 headless、无人值守的 Agent
- 高流量 Agent API（Virtual Sandbox 比容器快 10x+）

## 局限性

- 实验阶段，API 可能变化
- 2.9k stars，社区尚小
- 依赖 Astro 团队维护，非独立项目
- Daytona 容器模式需要额外 API Key 和费用

## 相关页面

- [[harness-engineering]] — Flue 是 Harness Engineering 的框架级实现
- [[knowledge-as-code]] — Flue 的 Markdown 驱动设计符合此趋势
- [[multica]] — 同类 Agent 平台，但更偏团队协作
- [[get-shit-done]] — 同类 AI 编程工具，但更偏个人项目管理
- [[agents-md]] — Flue 使用 AGENTS.md 定义 Agent 行为
