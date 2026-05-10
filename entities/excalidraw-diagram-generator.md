---
title: excalidraw-diagram-generator
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, agent, tool, design]
sources: [https://github.com/github/awesome-copilot/tree/main/skills/excalidraw-diagram-generator]
---

# excalidraw-diagram-generator

## Overview

来自 [[awesome-design-md]] 仓库（GitHub 官方 awesome-copilot）的 Agent 技能，能从自然语言描述生成 Excalidraw 格式图表。支持 9 种图表类型，输出 `.excalidraw` JSON 文件，可直接在 Excalidraw 或 VS Code 扩展中打开。安装量 16,000+。

## 仓库

- GitHub: [github.com/github/awesome-copilot](https://github.com/github/awesome-copilot)
- 路径: `skills/excalidraw-diagram-generator/`
- 安装: `npx skills add https://github.com/github/awesome-copilot --skill excalidraw-diagram-generator`

## 支持的 9 种图表类型

| 类型 | 适用场景 | 关键词 |
|------|---------|--------|
| 📊 流程图 (Flowchart) | 顺序流程、工作流、决策树 | workflow, process, steps |
| 🔗 关系图 | 实体关系、系统组件、依赖 | relationship, connections, dependencies |
| 🧠 思维导图 | 概念层级、头脑风暴、主题组织 | mind map, concepts, ideas |
| 🏗️ 架构图 | 系统设计、模块交互、数据流 | architecture, system, components |
| 📈 数据流图 (DFD) | 数据流转、数据处理过程 | data flow, data processing |
| 🏊 泳道图 (Swimlane) | 跨职能流程、角色分工 | business process, swimlane, actors |
| 📦 类图 (Class) | 面向对象设计、类结构关系 | class, inheritance, OOP |
| 🔄 时序图 (Sequence) | 对象交互、消息流、时间线 | sequence, interaction, messages |
| 🗃️ ER 图 | 数据库实体关系、数据模型 | database, entity, relationship |

## 核心工作流

### 六步生成流程

1. **理解需求** — 判断图表类型、关键元素、关系、复杂度
2. **选择图表类型** — 根据用户意图和关键词匹配
3. **提取结构化信息** — 不同图表类型提取不同要素（步骤/实体/分支等）
4. **生成 Excalidraw JSON** — 使用 `rectangle`、`ellipse`、`diamond`、`arrow`、`text` 元素
5. **格式化输出** — 标准 `.excalidraw` 文件格式（version 2）
6. **保存并告知** — 文件名 + 打开方式说明

### 关键技术要求

- 所有文本元素必须使用 `fontFamily: 5`（Excalifont）
- 每个元素需要唯一 ID（时间戳 + 随机字符串）
- 推荐元素数 < 20，超出建议拆分多图

## 布局参数

| 参数 | 推荐值 |
|------|--------|
| 水平间距 | 200-300px |
| 垂直间距 | 100-150px |
| 字体大小 | 16-24px |
| 主色（主要元素） | `#a5d8ff` 浅蓝 |
| 辅色（次要元素） | `#b2f2bb` 浅绿 |
| 强调色（中心/重要） | `#ffd43b` 黄色 |
| 警告色 | `#ffc9c9` 浅红 |

## 图标库集成（可选增强）

支持集成 Excalidraw 图标库（AWS、GCP、Azure 等），通过 Python 脚本自动注入图标，避免手动坐标计算和 token 浪费。

### 推荐方式：Python 脚本

```bash
# 添加图标
python scripts/add-icon-to-diagram.py diagram.excalidraw EC2 400 300 --label "Web Server"

# 添加箭头
python scripts/add-arrow.py diagram.excalidraw 300 250 500 300 --label "HTTPS"
```

优势：零 token 消耗、坐标自动计算、ID 自动管理、确定性结果。

### 图标库设置

1. 从 https://libraries.excalidraw.com/ 下载 `.excalidrawlib` 文件
2. 放入 `libraries/<name>/` 目录
3. 运行 `scripts/split-excalidraw-library.py` 拆分为单个图标文件
4. 生成 `reference.md` 索引 + `icons/*.json` 单独文件

## 内置资源

| 文件 | 说明 |
|------|------|
| `references/excalidraw-schema.md` | 完整 Excalidraw JSON Schema |
| `references/element-types.md` | 元素类型详细规格 |
| `templates/flowchart-template.json` | 流程图模板 |
| `templates/relationship-template.json` | 关系图模板 |
| `templates/mindmap-template.json` | 思维导图模板 |
| `scripts/split-excalidraw-library.py` | 图标库拆分工具 |
| `scripts/add-icon-to-diagram.py` | 图标注入脚本 |
| `scripts/add-arrow.py` | 箭头添加脚本 |

## 局限性

- 复杂曲线简化为直线/基础曲线
- 手绘粗糙度固定为 1
- 不支持内嵌图片自动生成
- 推荐最多 20 个元素/图
- 无自动碰撞检测

## 与同类工具对比

- vs [[baoyu-skills]] 中的 `baoyu-diagram`：baoyu 用 Claude 手写 SVG，本技能输出 Excalidraw JSON 格式
- vs Mermaid/PlantUML：本技能输出可编辑的图形化文件，而非代码渲染图
- vs [[huashu-design]]：huashu 偏向 HTML 原型，本技能专注矢量图表
