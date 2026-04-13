---
title: AI Image Generation Providers
created: 2026-04-12
updated: 2026-04-12
type: comparison
tags: [model, api, tool, inference]
sources: [raw/articles/baoyu-skills-readme-2026-04-12.md]
---

# AI Image Generation Providers

## Overview
AI 图像生成领域已形成多 provider 竞争格局。基于 [[baoyu-skills]] 中 `baoyu-imagine` 技能的 provider 支持情况，整理当前主流 API 服务商。

## Provider 对比

| Provider               | 代表模型                                  | 参考图支持           | 特点              |
| ---------------------- | ------------------------------------- | --------------- | --------------- |
| **OpenAI**             | gpt-image-1.5                         | ✅               | 质量稳定，Azure 部署可选 |
| **Google**             | gemini-3-pro-image-preview            | ✅               | 多模态原生支持         |
| **OpenRouter**         | google/gemini-3.1-flash-image-preview | ✅               | 统一入口，多模型可选      |
| **DashScope (阿里通义万相)** | qwen-image-2.0-pro                    | ✅               | 中文渲染强，自定义尺寸     |
| **Z.AI (智谱 GLM)**      | glm-image                             | ❌               | 中文海报/图表优秀       |
| **MiniMax**            | image-01 / image-01-live              | ✅ (人物一致性)       | 低延迟版本可选         |
| **Jimeng (即梦)**        | jimeng_t2i_v40                        | ❌               | 火山引擎            |
| **Seedream (豆包)**      | doubao-seedream-5.0                   | ✅ (5.0/4.5/4.0) | 字节系             |
| **Replicate**          | google/nano-banana-2 等                | ✅               | 开源模型托管          |

## 市场趋势
1. **多模态融合**: 图像生成逐渐成为 LLM 的内置能力（如 GPT-4o、Gemini）
2. **中文优化**: 国产 provider（DashScope、Z.AI、即梦）在中文文字渲染上有明显优势
3. **参考图/一致性**: 人物一致性（MiniMax）和风格迁移成为差异化竞争点
4. **统一接口**: 中间层（OpenRouter、baoyu-imagine）抽象多 provider，降低切换成本

## 创业机会
- **统一 API 网关**: 类似 OpenRouter 但专注图像领域，自动路由最佳 provider
- **中文内容工具链**: 微信/小红书场景下的图文生成一体化
- **一致性引擎**: 跨 provider 的角色/品牌一致性管理

## 相关页面
- [[baoyu-skills]] — 集成案例
- [[claude-code-skills]] — 工具分发渠道
