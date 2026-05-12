---
title: OpenFootball World Cup
created: 2026-05-12
updated: 2026-05-12
type: entity
tags: [data, open-source, tool]
sources: [https://github.com/openfootball/worldcup]
---

# OpenFootball World Cup

## 概述

OpenFootball World Cup 是 [football.db](http://openfootball.github.io) 开源项目的核心数据仓库，以人类可读的 **Football.TXT 纯文本格式**存储世界杯全部赛事数据。覆盖 **23 届男足世界杯**（1930-2026，含已编排的 2026 美加墨世界杯），提供比分、阵容、进球、换人、红黄牌等完整比赛记录。

该项目的核心理念是：**足球数据应该是免费、开放、公共领域的**，用纯文本而非数据库格式存储，使其可在任何编程语言中使用，且对 Git 友好（可 diff、可 merge）。

## 仓库信息

| 项目 | 详情 |
|------|------|
| 仓库 | https://github.com/openfootball/worldcup |
| 所属项目 | football.db — 开源公共足球数据库 |
| 许可证 | Public Domain（公共领域） |
| 格式 | Football.TXT（结构化纯文本） |
| 工具 | sportdb CLI（构建 SQLite 数据库） |
| 文件数 | 559 个 .txt 文件 |
| 覆盖范围 | 1930-2026 共 23 届世界杯 |

## 数据结构

仓库采用**分层数据架构**，同一届赛事有多个详细程度的数据层：

### 目录结构

```
worldcup/
├── 1930--uruguay/          # 每届世界杯一个目录（23个）
│   ├── cup.txt             # 小组赛分组 + 比赛结果
│   └── cup_finals.txt      # 淘汰赛 + 决赛
├── min/                    # 最小化版本（纯比分）
│   ├── 1930.txt
│   └── ...
├── more/                   # 完整版本（含阵容、换人、进球者）
│   ├── 1930.txt            # 比赛结果
│   ├── 1930_full.txt       # 完整比赛记录
│   └── 1930_squads.txt     # 球队阵容
├── rsssf/                  # RSSSF 原始数据存档
└── planetworldcup/         # Planet World Cup 转换数据
```

### Football.TXT 格式示例

```
= World Cup 2022       # in Qatar, November 20 - December 18

Group A  | Qatar      Ecuador       Senegal        Netherlands
Group B  | England    Iran          USA            Wales
...

▪ Group A
Sun Nov 20
  19:00      Qatar   v Ecuador  0-2 (0-2)    @ Al Bayt Stadium, Al Khor
               (Enner Valencia 16'(p), 31')
```

格式特点：
- `=` 开头标记赛事标题
- `Group X |` 标记小组分组
- `▪` 标记轮次/阶段
- `@` 标记城市/球场
- 比分后括号内为进球者和时间
- `a.e.t.` 表示加时赛，`pen.` 表示点球大战

### 数据层级对比

| 层级 | 目录 | 内容 | 用途 |
|------|------|------|------|
| 最小化 | `min/` | 仅比分 | 快速查询、教学 |
| 标准 | `{year}--{host}/` | 分组 + 比赛 + 淘汰赛 | 日常使用 |
| 完整 | `more/` | 含阵容、换人、进球细节 | 深度分析 |
| 原始 | `rsssf/` | RSSSF 源数据 | 数据溯源 |

## 核心特性

- **纯文本格式**：无需数据库、无需解析库，任何语言都能读取
- **Git 友好**：文本文件可 diff、merge、PR，天然支持版本控制和协作
- **多粒度数据**：从纯比分到完整阵容，按需选择详细程度
- **持续更新**：已包含 2026 美加墨世界杯分组和赛程
- **公共领域**：无任何版权限制，可自由使用
- **sportdb CLI**：一行命令构建 SQLite 数据库（`sportdb build`）
- **社区生态**：属于 openfootball 组织，涵盖联赛、杯赛等多个子项目

## 与其他世界杯数据库的对比

| 维度 | OpenFootball World Cup | [[fjelstul-worldcup-database]] |
|------|----------------------|-------------------------------|
| 格式 | Football.TXT 纯文本 | R 包 / CSV / JSON / SQLite |
| 覆盖年份 | 1930-2026（含未来赛事） | 1930-2022（男足）+ 1991-2019（女足） |
| 女足数据 | ❌ 无 | ✅ 8 届女足世界杯 |
| 数据粒度 | 比分/阵容/进球者/换人 | 27 个结构化数据集，158 万+数据点 |
| 数据验证 | 社区维护 | Wikipedia + FIFA 官方报告交叉验证 |
| 分析就绪度 | 需解析文本 | 即用型结构化表格 |
| Git 友好性 | ★★★★★（纯文本） | ★★★（二进制 RData） |
| 许可证 | Public Domain | CC-BY-SA 4.0 |

## 使用方式

```bash
# 方式一：使用 sportdb CLI 构建数据库
gem install sportdb
sportdb new worldcup    # 从模板构建
sportdb build           # 从本地文件构建

# 方式二：直接读取文本文件
cat 2022--qatar/cup.txt         # 查看分组
cat 2022--qatar/cup_finals.txt  # 查看淘汰赛

# 方式三：用 Python 解析
# Football.TXT 格式简单，正则即可解析
```

## football.db 生态

本仓库是 openfootball 组织的一部分，其他相关仓库包括：
- `openfootball/football.csv` — 联赛数据（CSV 格式）
- `openfootball/earth` — 全球足球数据集合
- `openfootball/quick-starter` — 快速启动模板

## 相关资源

- [[fjelstul-worldcup-database]] — 另一个综合性世界杯数据库，R/CSV/JSON/SQLite 格式，含女足数据
- [[public-apis]] — 公共 API 集合，类似的数据开放理念
