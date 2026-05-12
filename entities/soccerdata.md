---
title: SoccerData
created: 2026-05-12
updated: 2026-05-12
type: entity
tags: [data, open-source, tool]
sources: [https://github.com/probberechts/soccerdata]
---

# SoccerData

## 概述

SoccerData 是一个 Python 足球数据采集库，提供从 **8 个主流足球数据网站**抓取数据的统一接口，返回格式一致的 pandas DataFrame。核心优势是**跨数据源的统一列名和标识符**，以及**本地缓存机制**避免重复请求。

与 [[worldfootballr]]（R 包，已归档）定位相似，但 SoccerData 是 Python 生态、仍在活跃维护、数据源更多（8 个 vs 3 个）。

## 仓库信息

| 项目 | 详情 |
|------|------|
| 仓库 | https://github.com/probberechts/soccerdata |
| 文档 | https://soccerdata.readthedocs.io |
| 作者 | Pieter Robberechts（KU Leuven） |
| 版本 | 1.9.0 |
| 许可证 | Apache-2.0 |
| 语言 | Python（>=3.10, <3.15） |
| 状态 | ✅ 活跃维护 |
| PyPI | `pip install soccerdata` |

## 数据源（8 个）

| 数据源 | 类名 | 数据内容 | 特色 |
|--------|------|----------|------|
| [Club Elo](http://clubelo.com) | `ClubElo` | 球队 Elo 评分及历史 | 欧洲联赛，每轮更新 |
| [ESPN](https://www.espn.com/soccer/) | `ESPN` | 历史结果、统计、阵容 | 覆盖广泛 |
| [FBref](https://fbref.com/en/) | `FBref` | 比赛结果、阵容、球员/球队详细统计 | 基于 Opta 数据，最全面 |
| [Football-Data.co.uk](https://www.football-data.co.uk) | `MatchHistory` | 历史结果、赔率、比赛统计 | 含博彩数据 |
| [Sofascore](https://sofascore.com) | `Sofascore` | 赛程、排名、阵容、详细统计 | 实时数据 |
| [SoFIFA](https://sofifa.com) | `SoFIFA` | 球员能力评分、球队评分 | EA Sports FC 数据 |
| [Understat](https://understat.com) | `Understat` | xG、xGBuildup、xGChain、射门事件 | 高级统计 |
| [WhoScored](https://whoscored.com) | `WhoScored` | 比赛结果、预览、Opta 事件流数据 | Selenium 驱动 |

## 核心 API（各数据源 `read_*` 方法）

### FBref（最常用，9 个方法）

```python
fbref = sd.FBref('ENG-Premier League', '2021')
fbref.read_leagues()                    # 可用联赛列表
fbref.read_seasons()                    # 可用赛季列表
fbref.read_schedule()                   # 赛程
fbref.read_team_season_stats(stat_type="passing")   # 球队赛季统计
fbref.read_team_match_stats(...)        # 球队比赛统计
fbref.read_player_season_stats(stat_type="standard") # 球员赛季统计
fbref.read_player_match_stats(...)      # 球员比赛统计
fbref.read_lineup(...)                  # 阵容
fbref.read_events(...)                  # 比赛事件
```

### MatchHistory（Football-Data.co.uk）

```python
mh = sd.MatchHistory('ENG-Premier League', '2021')
mh.read_games()  # 比赛结果 + 赔率 + 统计
```

### Understat（xG 数据）

```python
us = sd.Understat('ENG-Premier League', '2021')
us.read_schedule()              # 赛程
us.read_team_match_stats()      # 球队比赛统计
us.read_player_season_stats()   # 球员赛季统计
us.read_shot_events()           # 射门事件（含 xG）
```

### SoFIFA（球员能力值）

```python
sofifa = sd.SoFIFA('ENG-Premier League', '2021')
sofifa.read_teams()          # 球队列表
sofifa.read_players()        # 球员能力评分
sofifa.read_team_ratings()   # 球队综合评分
sofifa.read_player_ratings() # 球员详细评分
```

### WhoScored（Opta 事件流）

```python
ws = sd.WhoScored('ENG-Premier League', '2021')
ws.read_schedule()      # 赛程
ws.read_events()        # Opta 事件流数据（传球、射门、控球等）
ws.read_missing_players()  # 缺阵球员
```

### Sofascore

```python
sc = sd.Sofascore('ENG-Premier League', '2021')
sc.read_league_table()  # 联赛排名
sc.read_schedule()      # 赛程
```

### ClubElo

```python
elo = sd.ClubElo('ENG-Premier League', '2021')
elo.read_by_date(date='2021-12-01')  # 某日所有球队 Elo
elo.read_team_history(team='Man City')  # 球队 Elo 历史
```

## 核心特性

- **统一接口**：8 个数据源用一致的 `read_*` 方法调用，返回 pandas DataFrame
- **统一列名**：跨数据源的列名和球队/球员标识符保持一致，便于合并分析
- **本地缓存**：数据下载后缓存在本地，避免重复请求
- **联赛/赛季抽象**：统一的联赛名和赛季编码，不需记忆各网站的 ID 系统
- **Selenium 支持**：WhoScored 等动态页面用 Seleniumbase 渲染
- **DVC 集成**：测试数据用 DVC 管理
- **活跃维护**：持续更新，适应网站结构变化

## 与其他足球数据工具对比

| 维度 | SoccerData | [[worldfootballr]] | [[fjelstul-worldcup-database]] | [[openfootball-worldcup]] |
|------|-----------|-------------------|-------------------------------|--------------------------|
| 语言 | Python | R | R/CSV/JSON/SQLite | 纯文本 |
| 类型 | 数据抓取库 | 数据抓取包 | 静态数据库 | 静态数据集 |
| 数据源数 | 8 个 | 3 个 | 1 个（Wikipedia+FIFA） | 1 个（Wikipedia+RSSSF） |
| 覆盖范围 | 全球联赛 | 全球联赛 | 仅世界杯 | 仅世界杯 |
| 维护状态 | ✅ 活跃 | ⚠️ 已归档 | ✅ 活跃 | ✅ 活跃 |
| 缓存 | ✅ 本地缓存 | ❌ | N/A | N/A |
| 统一列名 | ✅ | 部分 | N/A | N/A |

## 安装

```bash
pip install soccerdata

# 含 socceraction 集成（可选）
pip install soccerdata[socceraction]
```

## 局限性

- **依赖网站结构**：爬虫函数依赖各网站 HTML/API 结构，改动即失效
- **WhoScored 需要 Selenium**：需要浏览器驱动，部署环境要求更高
- **速率限制**：频繁请求可能被封 IP，需合理设置缓存
- **部分数据源不稳定**：FiveThirtyEight 已停止足球预测，部分功能可能失效

## 相关资源

- [[worldfootballr]] — R 版足球数据抓取包（已归档），3 个数据源
- [[fjelstul-worldcup-database]] — 世界杯专用结构化数据库
- [[openfootball-worldcup]] — 世界杯纯文本数据集
