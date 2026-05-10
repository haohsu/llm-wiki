---
title: mano-p
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [company, open-source, agent, model, inference, tool]
sources: [https://github.com/MININGLAMP-AI/MANO-P]
---

# Mano-P

## Overview

Mano-P 是明略科技（Mininglamp AI）开源的 **GUI-VLA（视觉-语言-动作）智能体模型**，专为边缘设备设计。"Mano"是西班牙语"手"的意思，P 代表 Private——核心理念是让个人和组织创建自己的私有 AI。项目在 OSWorld 基准测试中以 **58.2% 成功率排名第一**（专用 GUI 智能体模型），领先第二名 opencua-72b 达 13.2 个百分点。

- GitHub: [github.com/MININGLAMP-AI/MANO-P](https://github.com/MININGLAMP-AI/MANO-P)
- 论文: [arXiv:2509.17336](https://arxiv.org/abs/2509.17336)
- License: Apache 2.0
- 模型下载: [HuggingFace](https://huggingface.co/Mininglamp-2718/Mano-P) · [ModelScope](https://modelscope.cn/models/Mininglamp/Mano-P)
- 联系: model@mininglamp.com

## 核心能力

| 能力 | 说明 |
|------|------|
| 复杂 GUI 自动化 | 自主完成含数百个交互元素的界面操作 |
| 跨系统数据整合 | 纯视觉交互，无需 API 接口 |
| 长任务规划 | 支持数十至上百步的企业级业务流程 |
| 端侧原生推理 | Apple M4+ 本地运行，数据不出设备 |
| 智能报告生成 | 自动生成数据分析报告、工作总结等 |
| 自主应用构建 | Mano-AFK 驱动 PRD→代码→部署→测试→修复全流程 |

## 基准测试成绩

### GUI Grounding & CUA

| 基准 | Mano-P 成绩 | 对比 |
|------|------------|------|
| OSWorld（专用模型） | **58.2%**（72B） | #1，超 opencua-72b (45.0%) 13.2pp |
| OSWorld（全部模型） | 58.2% | Claude Sonnet 4.6 达 72.1%（通用模型） |
| WebRetriever Protocol I | **41.7 NavEval** | 超 Gemini 2.5 Pro CU (40.9)、Claude 4.5 CU (31.3) |

### 端侧推理性能

| 模型 | 芯片 | 量化 | Prefill | Decode |
|------|------|------|---------|--------|
| Mano-P 1.0-4B | Apple M5 Pro 64GB | W8A16 | 2.839s | 80.1 tok/s |
| Mano-P 1.0-4B | Apple M5 Pro 64GB | W8A8 (Cider) | 2.519s（↓12.7%） | 79.5 tok/s |

## 分阶段开源策略

Mano-P 面向三类开发者分阶段开源：

| 阶段 | 内容 | 目标用户 | 状态 |
|------|------|---------|------|
| Phase 1 | Mano-CUA Skills（GUI 自动化技能） | Agent 爱好者（OpenClaw / Claude Code 用户） | ✅ 已发布 |
| Phase 2 | 本地模型 + SDK（端侧推理组件） | 高安全性要求的开发者 | ✅ 已发布 |
| Phase 3 | 训练方法 + 剪枝/量化技术 | 需要定制模型的开发者 | 🔜 即将发布 |

## 技能系统 (Mano-Skill)

Mano-Skill 是基于 Mano 模型的桌面 GUI 自动化工具，提供两种使用形式：

### 1. mano-cua — CLI 命令行工具

面向人类用户（开发者），在终端直接执行 GUI 自动化任务。

```bash
# 安装
brew tap Mininglamp-AI/tap && brew install mano-cua

# 云端模式（默认）
mano-cua run "打开微信，告诉 FTY 会议推迟"

# 本地模式（数据不出设备）
mano-cua check          # 检查环境
mano-cua install-sdk    # 安装 SDK
mano-cua install-model  # 拉取模型
mano-cua run "打开 Safari 搜索 Python" --local
```

### 2. mano-skill — ClawHub Agent 技能

面向 AI 智能体（Claude Code、OpenClaw 等），Agent 在推理过程中自动调用 GUI 操作。

```bash
clawhub install mano-cua
```

用户对 Agent 说"帮我打开微信找 FTY 的聊天窗口告诉他会议推迟"，Agent 自动完成操作。

### 推理模式

| 模式 | 数据处理 | 适用场景 |
|------|---------|---------|
| 云端模式 | 截图+任务描述发送至 mano.mininglamp.com | 快速体验，无需本地模型 |
| 本地模式 | 全部在 Mac mini/MacBook 本地执行 | 高安全性场景，零网络调用 |

**硬件要求**：Apple M4+ 芯片，32GB+ RAM；或任意 Mac + Mano-P 算力棒（USB 4.0）

## 推理加速 SDK (Cider)

Cider 是基于 MLX 的 macOS 推理加速 SDK，补足了 MLX 缺失的 INT8 激活量化能力。

### 核心特性

| 特性 | 说明 |
|------|------|
| W8A8 量化 | 权重 INT8 + 激活 INT8，per-channel / per-group |
| W4A8 量化 | 权重 INT4 打包 + 激活 INT8 |
| 条件编译 | M5+ 编译 INT8 TensorOps C++ 扩展，M4 及以下回退纯 Python |
| 兼容性 | 非侵入式兼容 mlx_vlm（已验证 0.4.3），修复 Qwen3-VL 多图推理问题 |

### 性能提升（Apple M5 Pro）

| 模型 | 量化 | Prefill (tok/s) | 对比 FP16 |
|------|------|----------------|----------|
| Qwen3-VL-2B | W8A8 PC | **3242** | +7.7%（vs FP16 3010） |
| Qwen3-VL-4B | W8A8 PC | **2186** | +16.0%（vs FP16 1884） |
| Qwen3-8B (LLM) | W8A8 PC | Prefill 123.5s | **-31.3%**（vs FP16 179.9s） |
| Llama3-8B (LLM) | W8A8 PC | Prefill 123.3s | **-29.9%**（vs FP16 175.8s） |

- GitHub: [github.com/Mininglamp-AI/cider](https://github.com/Mininglamp-AI/cider)
- 不仅限于 Mano-P，可加速任何 MLX 模型

## 自主应用构建 (Mano-AFK)

Mano-AFK 是自主全周期应用构建器，从一句自然语言需求到部署、测试、修复的完整应用。

- GitHub: [github.com/Mininglamp-AI/mano-afk](https://github.com/Mininglamp-AI/mano-afk)
- ClawHub: [clawhub.ai/hanningwang/mano-afk](https://clawhub.ai/hanningwang/mano-afk)

工作流：需求澄清 → 架构设计 → 代码生成 → 本地部署 → 多级测试（API/LLM 视觉检查/GUI 自动化）→ 失败自动定位→修复→重试→通过

E2E 测试阶段默认使用 Mano-P 作为本地视觉后端（数据不出设备），也可切换至 Claude CUA 云端模式。

## 技术方法 (Mano-Action)

Mano-Action 是专为 GUI Grounding 设计的双向自增强训练框架：

- **双向循环学习**：Text→Action 和 Action→Text 互增强
- **三阶段渐进训练**：SFT → 离线强化学习 → 在线强化学习
- **闭环数据生成**：自动生成高质量训练数据
- **端侧优化适配**：量化、剪枝、边缘推理自适应
- **GSPruning**：视觉 Token 剪枝方法，2-3x 吞吐量提升

## 竞品对比

| 特性 | Mano-P | OpenClaw | Manus | 传统 RPA |
|------|--------|----------|-------|---------|
| 模型来源 | ✅ 内置端侧模型 | ⚠️ 用户配置 | ⚠️ 云端 API | ❌ 规则引擎 |
| 数据安全 | ✅ 本地执行 | ⚠️ LLM/技能云端调用 | ⚠️ 云端推理 | ✅ 可本地 |
| 控制方式 | ✅ 纯视觉 | ⚠️ CDP+CLI | ❌ HTML 解析+CLI | ❌ 系统 API |
| 适用场景 | ✅ 全类型 GUI | ✅ 多类型应用 | ⚠️ 仅 Web | ⚠️ 特定系统 |
| 长任务规划 | ✅ 自主规划 | ✅ 自主规划 | ✅ 可视化编排 | ❌ 需预设流程 |
| UI 变化适应 | ✅ 自适应 | ✅ LLM 自适应 | ⚠️ 有限 | ❌ 需重新配置 |

## 生态关系

- 与 [[claude-code-skills]] 生态紧密关联——mano-skill 可作为 Claude Code / OpenClaw 的技能安装
- Cider SDK 可独立用于任何 MLX 模型加速，不限于 Mano-P
- Mano-AFK 展示了 Agent 驱动的端到端软件构建范例

## 局限性

- 硬件要求较高：Apple M4+ 且 32GB+ RAM（或需算力棒）
- macOS 优先，Windows/Linux 处于 Beta 阶段
- 复杂曲线/3D 场景支持有限
- 单设备同时只能运行一个任务
- 仅支持主显示器
