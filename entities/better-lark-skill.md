---
title: better-lark-skill
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, agent, tool, platform]
sources: [https://github.com/psylch/better-lark-skill]
---

# better-lark-skill

## Overview

统一的飞书/Lark 全功能 CLI 技能，将原本 19 个独立的 lark-* skill 合并为一个模块化 skill，通过 [lark-cli](https://github.com/larksuite/cli) 一站式访问飞书全部功能。支持按需加载 reference 文档，共 **185 个 reference 文件**覆盖飞书所有模块。

- GitHub: [github.com/psylch/better-lark-skill](https://github.com/psylch/better-lark-skill)
- License: MIT
- 安装: `npx skills add psylch/better-lark-skill -g -y`
- 前置依赖: [lark-cli](https://github.com/larksuite/cli)（`npm install -g @larksuite/cli`）
- 兼容: Claude Code、Cursor、Windsurf 等支持 skills.sh 的 AI 编程 Agent

## 设计理念

- **合并 19 → 1**：将分散的 lark-* skill 统一为一个模块化 skill
- **按需加载**：SKILL.md 仅做模块路由，详细操作指引放在 185 个 reference 文件中
- **上下文感知**：根据用户意图自动路由到对应模块，读取对应 reference 后执行 lark-cli 命令

## 15 大模块

| 模块 | 说明 | 触发关键词 |
|------|------|-----------|
| 即时通讯 (IM) | 收发消息、管理群聊、搜索消息 | 消息、群聊、发消息、chat |
| 云文档 (Docs) | 从 Markdown 创建/编辑文档、搜索、插图 | 文档、创建文档、doc |
| 电子表格 (Sheets) | 读写表格、追加、导出、查找 | 表格、spreadsheet、sheets |
| 多维表格 (Base) | Bitable 全功能：表/字段/记录/视图/表单/仪表盘/工作流/角色 | 多维表格、base、bitable |
| 日历 (Calendar) | 日程管理、忙闲查询、时间推荐 | 日程、日历、会议、calendar |
| 任务 (Task) | 待办事项、任务清单、分配、评论、提醒 | 任务、待办、todo、task |
| 云空间 (Drive) | 上传下载文件、权限管理、评论 | 文件、上传、下载、drive |
| 邮箱 (Mail) | 收发邮件、转发、草稿、线程、监控（含安全规则） | 邮件、邮箱、mail、email |
| 通讯录 (Contact) | 搜索员工、获取用户信息、组织架构 | 搜索员工、通讯录、contact |
| 知识库 (Wiki) | 知识空间管理 | 知识库、wiki、空间 |
| 视频会议 (VC) | 会议记录搜索、纪要获取 | 会议记录、vc |
| 妙记 (Minutes) | AI 会议摘要 | 妙记、minutes |
| 画板 (Whiteboard) | 图表和可视化（架构图/柱状图/漏斗图/鱼骨图/甘特图等 14 种场景） | 画板、白板、图表、whiteboard |
| 事件订阅 (Event) | 实时事件监听 | 监听、事件、subscribe |
| 账号切换 (Switch) | 多账号 profile 管理、自动续命 token | 切换账号、switch、profile |

## 高级功能

### 工作流编排

预定义多步编排，组合多个模块完成复杂任务：

| 工作流 | 编排模块 | 说明 |
|--------|---------|------|
| 日程待办摘要 (Standup) | calendar + task | 生成指定日期的日程与未完成任务摘要 |
| 会议纪要整理 | vc + drive + docs | 汇总会议记录，生成结构化报告并创建文档 |

### OpenAPI 探索

当现有模块无法覆盖需求时，从飞书官方文档库逐层挖掘原生 OpenAPI 接口：
- 飞书: `https://open.feishu.cn/llms.txt`
- Lark: `https://open.larksuite.com/llms.txt`

### Skill 创建器

基于 lark-cli 创建新 Skill 的模板和指引，可将常用 API 调用封装为独立 skill。

## 认证与安全

```bash
lark-cli config init --new                    # 首次配置
lark-cli auth login --domain <domain>         # 用户身份登录
lark-cli auth status                          # 检查状态
bash ~/.lark-cli/switch.sh <profile>          # 切换账号（自动续命 token）
```

两种身份模式：`--as user`（用户资源）vs `--as bot`（应用级操作）

**安全规则**：
- 禁止输出密钥（appSecret、accessToken）到终端明文
- 写入/删除操作前必须确认用户意图
- 用 `--dry-run` 预览危险请求

## 多维表格 (Base) 深度覆盖

Base 模块是覆盖最深的子系统，包含 80+ reference 文件：

| 子模块 | 操作 |
|--------|------|
| 表 (Table) | 创建/获取/列表/更新/删除 |
| 字段 (Field) | 创建/获取/列表/更新/删除/搜索选项 |
| 记录 (Record) | 获取/列表/更新插入/删除/上传附件/历史 |
| 视图 (View) | 创建/获取/列表/重命名/删除 + 筛选/排序/分组/时间轴/卡片配置 |
| 表单 (Form) | 创建/获取/列表/更新/删除 + 问题管理 |
| 仪表盘 (Dashboard) | 创建/获取/列表/更新/删除 + Block 管理 |
| 工作流 (Workflow) | 创建/获取/列表/更新/启用/禁用/Schema |
| 角色 (Role) | 创建/获取/列表/更新/删除/配置 |
| 高级权限 | 启用/禁用 |
| 公式/查找字段指南 | 字段类型参考 |

## 画板 (Whiteboard) 场景模板

14 种预置图表场景：架构图、柱状图、对比图、鱼骨图、飞轮图、漏斗图、折线图、Mermaid、里程碑、组织架构、金字塔、树状图等。

## 生态关系

- 底层依赖 [lark-cli](https://github.com/larksuite/cli)（飞书官方 CLI 工具）
- 属于 [[claude-code-skills]] 生态中的飞书集成方案
- 与 [[baoyu-skills]] 中的发布技能（微信/微博/X）互补——本技能专注飞书内部协作
- 可作为 Agent 工作流中的飞书操作层，配合其他技能使用
