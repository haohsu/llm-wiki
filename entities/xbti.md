---
title: XBTI
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, tool, product]
sources: [https://github.com/lovstudio/XBTI]
---

# XBTI — 开源人格测试引擎

5 分钟创建你自己的 BTI 人格测试。源自 B 站 UP 主蛆肉儿串儿原创的 SBTI（恶搞版 MBTI），泛化后支持任意主题的人格测试生成。

- GitHub: [github.com/lovstudio/XBTI](https://github.com/lovstudio/XBTI)
- Stars: 3（引擎版）| 原始 SBTI 版 420 stars
- 语言: JavaScript（React 19 + Vite 8）
- 许可: Apache-2.0（代码），原创内容版权归 B站@蛆肉儿串儿
- 创建: 2026-04-09
- 作者: lovstudio.ai
- 原作者: [B站@蛆肉儿串儿](https://space.bilibili.com/417038183)

## 核心引擎

**15 维度评估 + 曼哈顿距离匹配算法**，只需添加一个 case 目录即可生成全新的人格测试。

### 已有变体

| 变体 | 主题 | 链接 |
|------|------|------|
| SBTI | 恶搞人格（27 种离谱人格） | [xbti.lovstudio.ai/c/sbti](https://xbti.lovstudio.ai/c/sbti) |
| CBTI | 猫猫人格 | [xbti.lovstudio.ai/c/cbti](https://xbti.lovstudio.ai/c/cbti) |

## 匹配算法

1. 每道题对应一个维度，同维度得分求和
2. 映射为三级：L（≤3）/ M（4）/ H（≥5）
3. 构建 15 维用户向量，与所有人格模式做**曼哈顿距离**匹配
4. 最近距离为匹配结果，相似度 = `(1 - distance/30) × 100%`
5. 兜底：相似度 < 60% 时强制分配到 fallback 人格

## 引擎架构

```
cases/                    # 各 BTI 变体数据
├── registry.js           # 注册所有变体
├── sbti/                 # SBTI 数据
│   ├── index.js          # meta 信息（id、名称、描述）
│   ├── dimensions.js     # 15 维度定义（5 模型 × 3 子维度）
│   ├── questions.js      # 30 道题（每维度 2 题，3 选项）
│   └── types.js          # 人格类型（代号、模式、描述）
└── cbti/                 # CBTI 数据（同结构）
src/
├── components/           # React 组件（首页/测试流程/结果页）
├── logic/scoring.js      # 通用匹配算法（无需修改）
└── useHashRoute.js       # 路由
```

## 创建你自己的 BTI

```bash
# 安装 Claude Code skill
npx skills add lovstudio/skills --skill lovstudio:xbti-creator

# 在 Claude Code 中调用
/lovstudio-xbti-creator
```

输入主题名和偏好，skill 自动生成完整的 BTI 变体（case 目录 + 数据文件）。

## 添加新 BTI 变体

1. 在 `cases/` 下新建目录
2. 填入数据文件：`index.js`（meta）+ `dimensions.js`（15 维度）+ `questions.js`（30 题）+ `types.js`（人格类型）
3. 在 `registry.js` 中注册

## 技术栈

| 层 | 技术 |
|---|------|
| 框架 | React 19 + Vite 8 |
| 包管理 | pnpm |
| 部署 | Vercel + Cloudflare DNS |

## 分支说明

| 分支 | 说明 |
|------|------|
| main | XBTI 引擎（泛化版，多 case 架构） |
| sbti | SBTI 原版（恶搞人格测试） |
| nbti | NBTI 版本（牛逼人格测试） |
| html-version | 最初的单文件 HTML 版 |

## 媒体报道

- [MBTI 过时了！XBTI"傻逼体"凭什么刷屏？](https://mp.weixin.qq.com/s/nXFvJrs_qqtrckmegSu2Zg)
- [MBTI 过时了，来 XBTI 测测吧...](https://mp.weixin.qq.com/s/XxYcBZzPLaQudK0cFFDgJQ)

## 适用场景

- 快速创建病毒传播人格测试
- 社交媒体营销内容
- 社区互动和用户参与
- AI 辅助生成测试内容（Claude Code skill）

## 局限性

- 引擎版仅 3 stars，社区尚小
- 原始 SBTI 版无 license，需注意版权
- 人格测试本质是娱乐，无科学依据
- 依赖 Vercel 部署

## 相关页面

- [[claude-code-skills]] — XBTI 的 xbti-creator skill 属于此生态
- [[knowledge-as-code]] — 人格测试数据结构化为代码的案例
