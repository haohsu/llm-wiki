---
title: decolua/9router
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, tool, api, product]
sources: [https://github.com/decolua/9router, https://github.com/decolua/9router/blob/master/README.zh-CN.md]
---

# 9Router — 免费 AI 路由器与 Token 节省器

将所有 AI 编程工具连接到 40+ AI 提供商和 100+ 模型的智能路由器。通过 RTK Token 节省器 + 自动切换到免费/低价模型，节省 20-40% tokens。

- GitHub: [github.com/decolua/9router](https://github.com/decolua/9router)
- Stars: 6,533
- 语言: JavaScript（Next.js）
- 许可: MIT
- npm: `npm install -g 9router`
- 网站: [9router.com](https://9router.com)
- 创建: 2026-01-05

## 核心价值

**问题：** 订阅配额到期未用、速率限制打断编程、工具输出（git diff/grep/ls）快速消耗 tokens、需要手动切换提供商。

**解决：**
- ✅ RTK Token 节省器 — 压缩 tool_result 内容，每次请求节省 20-40% tokens
- ✅ 智能三层切换 — 订阅 → 低价 → 免费，零停机时间
- ✅ 实时配额追踪 — 追踪 token 消耗，充分利用订阅价值
- ✅ 通用兼容 — 支持所有主流 AI 编程工具

## 工作原理

```
CLI 工具 (Claude Code/Codex/Cursor/Cline/...)
  ↓ http://localhost:20128/v1
9Router（智能路由器）
  ├─ RTK Token 节省器（减少 tool_result tokens）
  ├─ 格式转换（OpenAI ↔ Claude ↔ Gemini ↔ ...）
  ├─ 配额追踪 + 自动刷新 token
  ↓
三层路由：
  ├─ 第一层：订阅（Claude Code、Codex、GitHub Copilot）
  │   ↓ 配额耗尽
  ├─ 第二层：低价（GLM $0.6/1M、MiniMax $0.2/1M）
  │   ↓ 预算超限
  └─ 第三层：免费（Kiro、OpenCode Free、Vertex $300 额度）
```

## 主要功能

| 功能 | 作用 | 效果 |
|------|------|------|
| RTK Token 节省器 | 压缩工具输出（git diff/grep/ls/tree） | 节省 20-40% 输入 tokens |
| Caveman 模式 | 注入简洁提示词，保留技术实质 | 节省高达 65% 输出 tokens |
| 智能三层切换 | 自动路由：订阅→低价→免费 | 编程永不停歇 |
| 实时配额追踪 | token 计数 + 重置倒计时 | 充分利用订阅 |
| 格式转换 | OpenAI↔Claude↔Gemini↔Cursor↔Kiro↔Vertex | 兼容任何 CLI |
| 多账户支持 | 每个提供商多个账户 | 负载均衡+冗余 |
| 自动 Token 刷新 | OAuth token 自动刷新 | 无需手动重新登录 |
| 自定义组合 | 创建无限模型组合 | 自定义切换策略 |
| 云同步 | 跨设备同步配置 | 处处相同设置 |
| 使用分析 | 追踪 tokens/成本/趋势 | 优化开支 |

## 支持的 CLI 工具

Claude Code、OpenClaw、Codex、OpenCode、Cursor、Antigravity、Cline、Continue、Droid、Roo、Copilot、Kilo Code

## 支持的提供商（40+）

### OAuth 提供商
Claude Code、Antigravity、Codex、GitHub、Cursor

### 免费提供商
- Kiro AI — Claude 4.5 + GLM-5 + MiniMax，无限免费
- OpenCode Free — 无需认证，自动获取模型，无限免费
- Vertex AI — Gemini 3 Pro + GLM-5 + DeepSeek，$300 免费额度

### API Key 提供商（40+）
OpenRouter、GLM、Kimi、MiniMax、OpenAI、Anthropic、Gemini、DeepSeek、Groq、xAI、Mistral、Perplexity、Together AI、Fireworks、Cerebras、Cohere、NVIDIA、SiliconFlow、Nebius、Chutes、Hyperbolic 等

## 价格一览

| 等级 | 提供商 | 成本 | 适用场景 |
|------|--------|------|----------|
| 🚀 Token 节省器 | RTK（内置） | 免费 | 每次请求节省 20-40% |
| 💳 订阅 | Claude Code/Codex/Copilot/Cursor | $10-200/月 | 已有订阅的用户 |
| 💰 低价 | GLM ($0.6/1M)、MiniMax ($0.2/1M)、Kimi ($9/月) | 极低 | 预算备份 |
| 🆓 免费 | Kiro AI、OpenCode Free、Vertex AI | $0 | 零成本编程 |

**专业提示：** RTK + Kiro AI + OpenCode Free = $0 成本 + 节省 20-40% tokens

## 安装

```bash
# 全局安装
npm install -g 9router

# 启动
9router
# 控制面板: http://localhost:20128
# API 端点: http://localhost:20128/v1

# 从源码运行
git clone https://github.com/decolua/9router.git
cd 9router
cp .env.example .env
npm install
PORT=20128 npm run dev
```

## 部署方式

- 💻 本地 — 默认，离线可用
- ☁️ VPS/云 — 跨设备共享
- 🐳 Docker — 一键部署
- 🚀 Cloudflare Workers — 全球边缘网络

## 生态关系

- 与 [[claude-code-skills]] 生态深度集成——作为所有 AI 编程工具的统一网关
- 与 [[tavily-ai-skills]] 互补——9Router 管理 LLM 请求路由，Tavily 管理 Web 搜索
- 集成了 RTK（rtk-ai/rtk, 40K stars）和 Caveman（JuliusBrussee/caveman, 52K stars）两个开源项目
- 定位为 AI 编程工具的"基础设施层"——在 CLI 工具和 AI 提供商之间做智能路由
