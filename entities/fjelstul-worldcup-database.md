---
title: Fjelstul World Cup Database
created: 2026-05-12
updated: 2026-05-12
type: entity
tags: [data, open-source, tool]
sources: [https://github.com/jfjelstul/worldcup]
---

# Fjelstul World Cup Database

## 概述

Fjelstul World Cup Database 是由 Joshua C. Fjelstul 博士创建的综合性 FIFA 世界杯数据库，覆盖全部 **22 届男足世界杯**（1930-2022）和 **8 届女足世界杯**（1991-2019）。数据库包含 **27 个数据集、超过 158 万个数据点**，涵盖赛事、球队、球员、教练、裁判、进球、红黄牌、换人等世界杯所有维度。

该数据库被 Washington Post、FiveThirtyEight、The Markup、Data is Plural、The Times、AFP、Barron's、Hindustan Times、DataCamp 等知名媒体和数据平台引用。

## 仓库信息

| 项目 | 详情 |
|------|------|
| 仓库 | https://github.com/jfjelstul/worldcup |
| 作者 | Joshua C. Fjelstul, Ph.D. |
| 许可证 | CC-BY-SA 4.0 |
| 语言 | R |
| 数据格式 | R 包 (.RData)、CSV、JSON、SQLite |
| 数据来源 | Wikipedia + FIFA 官方比赛报告交叉验证 |

## 数据集架构（5 大分组）

### 第一组：基础实体（9 个数据集）

| 数据集 | 记录数 | 变量数 | 说明 |
|--------|--------|--------|------|
| `tournaments` | 30 | 18 | 赛事信息：东道主、冠军、日期、赛制 |
| `confederations` | 6 | 5 | FIFA 六大洲际联合会 |
| `teams` | 88 | 14 | 参赛队伍：ISO 国家码、足协、联合会 |
| `players` | 10,401 | 13 | 球员：姓名、生日、Wikipedia 链接 |
| `managers` | 475 | 7 | 教练：姓名、国籍、Wikipedia 链接 |
| `referees` | 493 | 10 | 裁判：国籍、联合会 |
| `stadiums` | 240 | 8 | 比赛场馆：城市、容量 |
| `matches` | 1,248 | 38 | 比赛：主客队、比分、阶段、加时/点球 |
| `awards` | 8 | 5 | 个人奖项定义（金靴、金球等） |

### 第二组：赛事-人员映射（4 个数据集）

| 数据集 | 记录数 | 说明 |
|--------|--------|------|
| `qualified_teams` | 625 | 参赛队伍及最终成绩 |
| `squads` | 13,843 | 球员大名单：位置、球衣号码 |
| `manager_appointments` | 637 | 教练任命（含联合教练） |
| `referee_appointments` | 668 | 裁判任命（仅主裁） |

### 第三组：比赛出场映射（4 个数据集）

| 数据集 | 记录数 | 说明 |
|--------|--------|------|
| `team_appearances` | 2,496 | 球队出场：主客、进球、胜负 |
| `player_appearances` | 27,432 | 球员出场（1970 年起） |
| `manager_appearances` | 2,538 | 教练出场 |
| `referee_appearances` | 1,248 | 裁判出场 |

### 第四组：比赛事件（4 个数据集）

| 数据集 | 记录数 | 说明 |
|--------|--------|------|
| `goals` | 3,637 | 进球：球员、时间、类型（运动战/点球/乌龙） |
| `penalty_kicks` | 396 | 点球大战（不含常规时间点球） |
| `bookings` | 3,178 | 红黄牌（1970 年起） |
| `substitutions` | 10,222 | 换人（1970 年起） |

### 第五组：赛事属性（6 个数据集）

| 数据集 | 记录数 | 说明 |
|--------|--------|------|
| `host_countries` | 31 | 东道主及表现 |
| `tournament_stages` | 1,555 | 赛事阶段（小组赛/淘汰赛） |
| `groups` | 117 | 小组分组 |
| `group_standings` | 626 | 小组排名 |
| `tournament_standings` | 120 | 最终排名（前四名） |
| `award_winners` | 200 | 获奖球员 |

## 核心特性

- **时间跨度大**：从 1930 年首届到 2022 年卡塔尔世界杯，横跨近百年
- **男女足覆盖**：同时包含男足（22 届）和女足（8 届）数据
- **多格式输出**：R 包、CSV、JSON、SQLite 四种格式，适合不同使用场景
- **关系型设计**：SQLite 版本提供主键/外键，支持灵活的表关联查询
- **数据质量高**：基于 Wikipedia 抓取 + FIFA 官方报告交叉验证
- **完整复现代码**：提供 R 语言复现脚本，从 Wikipedia 页面抓取到数据库构建全流程可追溯
- **教学友好**：丰富的实体关系和多粒度分析单元，适合数据科学教学

## 数据注意事项

- **球员姓名**：FIFA 官方报告存在大量拼写错误，本数据库使用 Wikipedia 更正后的版本
- **球衣号码**：1954 年之前球员不固定球衣号码，`shirt_number` 为 0
- **换人数据**：1970 年之前 FIFA 比赛报告不记录换人信息
- **时间格式**：分钟从 1' 开始（1' = 00:00-00:59），补时用 `+` 表示（如 45'+2'）
- **国家代码**：使用 ISO Alpha-3，英格兰用 ENG 而非 GBR，前南斯拉夫用 YUG

## 使用方式

```r
# R 包安装
devtools::install_github("jfjelstul/worldcup")
library(worldcup)

# 示例：查看所有比赛
data(matches)

# 示例：查看球员数据
data(players)
```

```python
# Python 直接读取 CSV
import pandas as pd
goals = pd.read_csv("data-csv/goals.csv")
matches = pd.read_csv("data-csv/matches.csv")
```

## 引用

> Fjelstul, Joshua C. "The Fjelstul World Cup Database v.1.2.0." July 19, 2023.
> https://www.github.com/jfjelstul/worldcup.

## 相关资源

- [[public-apis]] — 公共 API 集合，类似的数据开放理念
- [[codebase-to-course]] — 代码仓库转教程，可用于学习该数据库的使用
