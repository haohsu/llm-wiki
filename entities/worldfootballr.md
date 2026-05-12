---
title: worldfootballR
created: 2026-05-12
updated: 2026-05-12
type: entity
tags: [data, open-source, tool]
sources: [https://github.com/JaseZiv/worldfootballR]
---

# worldfootballR

## 概述

worldfootballR 是一个 R 语言包，提供从 **FBref**（StatsPerform Opta）、**Transfermarkt** 和 **Understat** 三大足球数据网站抓取和清洗数据的统一接口。包内封装了 **75 个导出函数**，覆盖比赛结果、球员统计、球队统计、转会记录、市场估值、射门热图、阵容、伤病、停赛等几乎所有足球数据维度。

> ⚠️ **已归档（Archived）**：该包已停止维护。作者感谢社区多年支持后正式关闭项目。

## 仓库信息

| 项目 | 详情 |
|------|------|
| 仓库 | https://github.com/JaseZiv/worldfootballR |
| 作者 | Jason Zivkovic |
| 版本 | 0.6.8.0001（开发版） |
| 许可证 | GPL-3 |
| 语言 | R |
| 状态 | ⚠️ 已归档，不再维护 |
| CRAN | 版本过旧，建议从 GitHub 安装 |
| 文档 | https://jaseziv.github.io/worldfootballR/ |

## 数据源

| 数据源 | 覆盖内容 | 函数前缀 |
|--------|----------|----------|
| **FBref**（StatsPerform Opta） | 比赛结果、球员/球队统计、射门、阵容、高级统计、工资 | `fb_*` |
| **Transfermarkt** | 转会记录、市场估值、伤病、停赛、合同到期、教练历史 | `tm_*` |
| **Understat** | 射门位置、xG 数据、比赛统计、球员数据 | `understat_*` |

## 核心功能（75 个导出函数）

### FBref 数据（`fb_*`，约 30 个函数）

| 函数 | 用途 |
|------|------|
| `fb_match_results()` | 比赛结果 |
| `fb_match_stats()` | 单场比赛统计 |
| `fb_advanced_match_stats()` | 高级比赛统计（传球、射门等） |
| `fb_match_shooting()` | 射门数据 |
| `fb_match_lineups()` | 比赛阵容 |
| `fb_match_summary()` | 比赛摘要 |
| `fb_player_season_stats()` | 球员赛季统计 |
| `fb_player_scouting_report()` | 球员侦察报告 |
| `fb_player_goal_logs()` | 球员进球记录 |
| `fb_player_match_logs()` | 球员比赛记录 |
| `fb_player_info()` | 球员基本信息 |
| `fb_team_match_stats()` | 球队比赛统计 |
| `fb_team_player_stats()` | 球队球员统计 |
| `fb_big5_advanced_season_stats()` | 五大联赛高级赛季统计 |
| `fb_squad_wages()` | 球队工资数据 |
| `fb_league_urls()` | 联赛 URL 列表 |
| `fb_match_urls()` | 比赛 URL 列表 |
| `fb_player_urls()` | 球员 URL 列表 |

### Transfermarkt 数据（`tm_*`，约 15 个函数）

| 函数 | 用途 |
|------|------|
| `player_market_values()` | 球员市场估值 |
| `player_transfer_history()` | 球员转会历史 |
| `tm_team_transfers()` | 球队转入/转出 |
| `tm_team_transfer_balances()` | 球队转会收支 |
| `tm_player_bio()` | 球员个人信息 |
| `tm_player_injury_history()` | 球员伤病历史 |
| `tm_player_absence()` | 球员缺阵记录 |
| `tm_league_injuries()` | 联赛伤病汇总 |
| `tm_league_suspensions()` | 联赛停赛汇总 |
| `tm_expiring_contracts()` | 即将到期合同 |
| `tm_league_debutants()` | 联赛新秀 |
| `tm_matchday_table()` | 联赛排名 |
| `tm_squad_stats()` | 球队阵容统计 |
| `tm_staff_job_history()` | 教练工作历史 |
| `tm_team_staff_history()` | 球队教练历史 |

### Understat 数据（`understat_*`，约 5 个函数）

| 函数 | 用途 |
|------|------|
| `understat_match_stats()` | 比赛统计（含 xG） |
| `understat_match_players()` | 比赛球员数据 |
| `understat_match_results()` | 比赛结果 |
| `understat_shots()` | 射门位置数据 |
| `understat_teams()` | 球队统计 |

### 预抓取数据加载（`load_*`）

v0.5.3 起支持通过 `load_` 函数快速加载预抓取数据，数据存储在 [worldfootballR_data](https://github.com/JaseZiv/worldfootballR_data) 仓库。

## 支持的联赛

**FBref**：全球主要联赛和杯赛，详见 [competitions.csv](https://github.com/JaseZiv/worldfootballR_data/blob/master/raw-data/all_leages_and_cups/all_competitions.csv)

**Transfermarkt**：主要联赛转会和估值数据，详见 [main_comp_seasons.csv](https://github.com/JaseZiv/worldfootballR_data/blob/master/raw-data/transfermarkt_leagues/main_comp_seasons.csv)

**Understat**：EPL、La Liga、Bundesliga、Serie A、Ligue 1、RFPL

## 使用示例

```r
library(worldfootballR)

# 获取英超 2023 赛季比赛结果
matches <- fb_match_results(country = "ENG", gender = "M",
                            season_end_year = 2023, tier = "1st")

# 获取球员市场估值
values <- player_market_values(country_name = "England",
                                start_year = 2023)

# 获取 xG 射门数据
shots <- understat_shots(match_url = "https://understat.com/match/12345")

# 快速加载预抓射数据
fb_data <- load_fb_match_results(country = "ENG", gender = "M",
                                  tier = "1st", season_end_year = 2023)
```

## 与其他足球数据库的关系

| 维度 | worldfootballR | [[fjelstul-worldcup-database]] | [[openfootball-worldcup]] |
|------|---------------|-------------------------------|--------------------------|
| 类型 | 数据抓取 R 包 | 静态数据库 | 静态文本数据集 |
| 覆盖范围 | 全球联赛+杯赛 | 仅世界杯 | 仅世界杯 |
| 数据源 | FBref/Transfermarkt/Understat | Wikipedia+FIFA | Wikipedia+RSSSF |
| 更新方式 | 实时抓取 | 手动更新 | 社区维护 |
| 格式 | R 数据框 | R/CSV/JSON/SQLite | Football.TXT |
| 维护状态 | ⚠️ 已归档 | ✅ 活跃 | ✅ 活跃 |

## 局限性

- **已停止维护**：不再更新，数据源网站结构变化可能导致函数失效
- **CRAN 版本过旧**：只能从 GitHub 安装最新版
- **依赖网站结构**：爬虫函数依赖 FBref/Transfermarkt/Understat 的 HTML 结构，任何改动都会导致失败
- **速率限制**：频繁抓取可能被数据源网站封禁
- **FotMob 已移除**：v0.6.4 起因 FotMob 服务条款变更不再支持

## 相关资源

- [[fjelstul-worldcup-database]] — 世界杯专用结构化数据库，R/CSV/JSON/SQLite 格式
- [[openfootball-worldcup]] — 世界杯纯文本数据集，Football.TXT 格式
