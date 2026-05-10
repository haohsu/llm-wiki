---
title: Awesome Happy Horse
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [tool, product, open-source]
sources: [https://github.com/ZeroLu/awesome-happy-horse]
---

# Awesome Happy Horse

Happy Horse 1.0 的社区策划资源集合——精选提示词、基准测试、样本视频，按真实创意用例分类组织。

## 概览

[ZeroLu](https://github.com/ZeroLu) 维护的 awesome list，汇集 X（Twitter）上顶级创作者的 Happy Horse 1.0 提示词和高质量样本视频。不同于常见的"长列表式"资源汇总，该仓库按实际创意场景分类，方便创作者快速找到参考案例。截至 2026-04-15 最后更新，已积累 75 stars。

## 基本信息

| 项目 | 详情 |
|------|------|
| 仓库 | [ZeroLu/awesome-happy-horse](https://github.com/ZeroLu/awesome-happy-horse) |
| Stars | 75 |
| Forks | 10 |
| 许可证 | CC BY 4.0 |
| 创建时间 | 2026-04-09 |
| 最后更新 | 2026-04-15 |
| 官网 | [happyhorseone.com](https://happyhorseone.com) |

## 内容分类

仓库将提示词和样本视频分为 5 大类别：

| 类别 | 说明 | 典型示例 |
|------|------|----------|
| **Film & Cinematic Storytelling** | 电影级叙事，追踪镜头、延时摄影、洞穴探索等 | Cave Flashlight Cinematic、Flower Time-Lapse、Tracking Shot Street Escape |
| **Advertising & Product Storytelling** | 产品广告叙事，家庭场景、品牌故事 | Voice Assistant Day-In-The-Life |
| **Animation & Stylized Visuals** | 动画与风格化视觉，赛博朋克、90年代卡通等 | 1990s Action Cartoon Firebending、Cyberpunk Android Repair Bay |
| **Social, Viral & UGC-Style Concepts** | 社交传播、病毒式 UGC 内容 | Graduation Banner Chaos |
| **Benchmark & Community Reference Reels** | 基准对比与社区样本集 | HappyHorse vs Seedance、Wildminder 对比、GENEL 对比 |

## 提示词特点

仓库中的提示词呈现以下共性特征：

- **英文为主**：绝大多数提示词为英文，少数有中文社区样本
- **细节丰富**：包含镜头运动（TRACKING SHOT、CLOSE-UP）、光照描述、材质细节
- **音频指令**：许多提示词包含 `Audio:` 段落，指定环境音效
- **风格锚定**：明确指定视觉风格（cyberpunk anime、1990s action cartoon 等）
- **场景完整性**：描述完整场景而非单一元素，适合生成连贯视频

## 基准测试

仓库收录了多个社区基准对比视频：

- HappyHorse vs Seedance（正面比较）
- Wildminder: HappyHorse-1.0 vs All（多模型横评）
- GENEL: HappyHorse vs Seedance 2.0（最新版本对比）
- GMI Cloud: Seedance 2.0 Comparison Challenge

这些对比主要评估运动一致性、输出质量和提示词遵循度。

## 标签体系

仓库使用的 GitHub Topics：`ai-video`、`happy-horse`、`happy-horse-1`、`text-to-video`、`image-to-video`、`video-generator`、`prompt-engineering`

## 生态关系

- [[awesome-seedance]] — 同类 awesome list，聚焦 Seedance 2.0 提示词，两者形成竞品提示词参考对照
- [[seedance-product-video]] — Seedance 产品视频技能，可与 Happy Horse 提示词互参
- [[ai-image-generation]] — AI 图像/视频生成 provider 全景，Happy Horse 是其中新兴竞争者

## 局限性

- 仓库较新（2026-04 创建），内容量有限，主要依赖少数几位 X 创作者的贡献
- 视频样本托管在 GitHub user-attachments 上，可能因存储策略变化而失效
- 缺少 Happy Horse 模型本身的技术文档链接（架构、训练数据等）
- 许可证为 CC BY 4.0，仅覆盖仓库内容，不涉及 Happy Horse 模型的使用条款
