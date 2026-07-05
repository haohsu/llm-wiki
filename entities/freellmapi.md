---
title: FreeLLMAPI
created: 2026-07-05
updated: 2026-07-05
type: entity
tags: [open-source, tool, product, api, agent]
sources: [raw/articles/freellmapi-README.md]
---

# FreeLLMAPI

聚合 18 个 LLM 提供商免费层的 OpenAI 兼容代理。将 Google、Groq、Cerebras、Mistral、OpenRouter 等 18 个平台 ~161 个免费模型统一到一个 `/v1` 端点，智能路由 + 自动故障转移。

- **GitHub**: https://github.com/tashfeenahmed/freellmapi
- **Stars**: 15,120 | **Forks**: 2,204
- **语言**: TypeScript
- **许可**: MIT
- **官网**: https://freellmapi.co
- **安装**: `curl -fsSL https://freellmapi.co/install.sh | bash`

> 聚合免费层：Google、Groq、Cerebras、NVIDIA、Mistral、OpenRouter、GitHub Models、Cohere、Cloudflare、HuggingFace、Z.ai（智谱）、Ollama Cloud、Kilo、Pollinations、LLM7、OVH AI Endpoints、OpenCode Zen、AI Horde
>
> + 自定义 OpenAI 兼容端点（llama.cpp、LM Studio、vLLM、Ollama 等）

## 核心理念

每个 AI 公司的免费层各自是小玩具。但 18 个叠在一起 ≈ **~1.7B tokens/月** 的工作推理容量，覆盖 160+ 模型。手动叠的问题是：18 套 SDK、18 套速率限制、18 个可能失败的地方。FreeLLMAPI 用一个 OpenAI 兼容端点全包了。

## 关键特性

| 特性 | 说明 |
|------|------|
| OpenAI 兼容 | `POST /v1/chat/completions` — 任何 OpenAI SDK 改 `base_url` 即可 |
| Anthropic 兼容 | `POST /v1/messages` — Claude Code / Anthropic SDK 可直接使用 |
| Responses API | `POST /v1/responses` — Codex CLI 的 wire format |
| Editor 补全 | `POST /v1/completions` — VS Code / Continue 内联建议 |
| 图片/语音 | `POST /v1/images/generations` + `/v1/audio/speech` |
| 嵌入向量 | `/v1/embeddings` — 同模型族故障转移 |
| 自动故障转移 | 429/5xx/超时 → 跳过 → 冷却 → 重试下个模型（最多 20 次）|
| 速率追踪 | 每个 (平台, 模型, key) 的 RPM/RPD/TPM/TPD 计数器 |
| 粘性会话 | 多轮对话 30 分钟内锁定同一模型 |
| 密钥加密 | AES-256-GCM 加密存储 |
| 统一 API key | 一个 `freellmapi-...` token 保护所有上游 key |
| 模型目录自更新 | 每天拉 2 次签名目录，新模型/配额变化自动落地 |
| 管理面板 | React + Vite UI，暗色模式，Playground |
| 分析 | 每请求日志：延迟、token 数、成功率、按提供商统计 |
| Docker | 多架构（amd64 + arm64），Raspberry Pi 可用 |
| 桌面应用 | macOS .dmg + Windows .exe 安装包 |

## 支持的提供商

| 提供商 | 代表模型 |
|--------|---------|
| **Google** | Gemini 2.5 Flash, 3.x previews |
| **Groq** | Llama 3.3, Llama 4, GPT-OSS, Qwen3 |
| **Cerebras** | Qwen3 235B |
| **OpenCode Zen** | DeepSeek V4 Flash, Nemotron (promo) |
| **Mistral** | Large 3, Medium 3.5, Codestral, Devstral |
| **OpenRouter** | 21 个免费层模型 |
| **GitHub Models** | GPT-4.1, GPT-4o |
| **Cloudflare** | Kimi K2, GLM-4.7, GPT-OSS, Granite 4 |
| **Cohere** | Command R+, Command-A (trial) |
| **Z.ai (智谱)** | GLM-4.5, GLM-4.7 Flash |
| **NVIDIA** | NIM, 40 RPM (eval-only ToS) |
| **HuggingFace** | Router → DeepSeek V4, Kimi K2.6, Qwen3 |
| **Ollama Cloud** | GLM-4.7, Kimi K2, gpt-oss, Qwen3 |
| **Kilo Gateway** | 免费路由（匿名可用） |
| **Pollinations** | GPT-OSS 20B（匿名可用） |
| **LLM7** | GPT-OSS, Llama 3.1, GLM（匿名可用） |
| **OVH AI Endpoints** | Qwen3.5 397B, GPT-OSS, Llama 3.3（匿名可用） |
| **AI Horde** | 社区 Llama, Gemma, Cydonia（匿名/慢速） |

## 商业模式

开源 MIT，但模型目录分两级：

| | Free | Premium |
|---|---|---|
| 价格 | $0, 永久 | **$19/年** 或 **$49 永久** |
| 模型数量 | 82 | **161** |
| 新模型延迟 | 上线 30 天后 | **当天** |
| 配额/修复 | 30 天滞后 | 2-3 天 |

Premium 用于资助日常模型测试和目录维护。服务器从不接触用户的 prompt/补全/密钥。

## 与 [[9router]] 的对比

| 维度 | FreeLLMAPI | 9router |
|------|-----------|---------|
| Stars | 15k | 6.5k |
| 定位 | 聚合免费层 LLM | AI 路由器 + Token 节省 |
| 提供商 | 18 个免费层 | 40+ 提供商 |
| 核心价值 | 一个端点聚合免费层 | 40+ 提供商路由 + RTK 节省 |
| 免费模型 | 161 | 不限 |
| 桌面 app | ✅ | ❌ |
| Anthropic 兼容 | ✅ | ❌ |

## 安装方式

```bash
# 一键安装（Docker）
curl -fsSL https://freellmapi.co/install.sh | bash

# 或 Docker Compose
git clone https://github.com/tashfeenahmed/freellmapi.git
cd freellmapi
openssl rand -hex 32 > .env  # 生成加密密钥
docker compose up -d

# 或用桌面 app（macOS/Windows）
# 从 Releases 下载 .dmg 或 .exe
```

## 适用场景

- **个人开发者**：一个端点用遍主流免费模型
- **AI 编程**：Claude Code、Codex、Continue 等指向本地 FreeLLMAPI
- **实验/原型**：零成本测试不同提供商的模型质量
- **本地方案**：连接本地 Ollama/llama.cpp + 云端免费层混合路由

## 局限性

- 单用户设计，无多租户
- 不支持 `/v1/moderations`
- 不支持 `n > 1`（单请求多补全）
- 免费层模型目录比 Premium 滞后 30 天
- 较新的模型（如 Kimi K2.7 Code、GLM-5.2）仅 Premium 可用

## 相关页面

- [[9router]] — 同类 AI 路由工具（40+ 提供商，Token 节省）
- [[openrouter]] — FreeLLMAPI 上游提供商之一
- [[hermes-agent]] — 兼容 FreeLLMAPI 作为后端
- [[claude-code-skills]] — FreeLLMAPI 支持 Anthropic API 供 Claude Code 使用
- [[llama-cpp]] — 可作为 FreeLLMAPI 的自定义提供商
- [[harness-engineering]] — FreeLLMAPI 是 Agent Harness 的"LLM 基础设施"组件
