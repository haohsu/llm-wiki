---
title: EKKOLearnAI/hermes-web-ui
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, tool, product, agent]
sources: [https://github.com/EKKOLearnAI/hermes-web-ui]
---

# Hermes Web UI

Hermes Agent 的全功能 Web 控制面板。管理 AI 聊天会话、监控用量与成本、配置平台频道、调度定时任务、浏览技能——全部通过一个干净、响应式的 Web 界面完成。

- GitHub: [github.com/EKKOLearnAI/hermes-web-ui](https://github.com/EKKOLearnAI/hermes-web-ui)
- Stars: 4,177
- 语言: TypeScript
- 许可: MIT
- npm: `npm install -g hermes-web-ui`
- 创建: 2026-04-11
- 作者: EKKOLearnAI (ekko8888)

## 定位

Hermes Agent 的官方 Web 前端。Hermes Agent 是一个多平台 AI 聊天系统，hermes-web-ui 为其提供浏览器端的完整管理界面。

## 架构

```
Browser → BFF (Koa, :8648) → Hermes Gateway (:8642)
                ↓
           Hermes CLI (sessions, logs, version)
                ↓
           ~/.hermes/config.yaml  (channel behavior)
           ~/.hermes/auth.json    (credential pool)
```

- **前端:** Vue 3 + TypeScript + Vite + Naive UI + Pinia + vue-i18n + SCSS
- **后端:** Koa 2 BFF + node-pty (Web Terminal)
- **设计:** 多 Agent 可扩展——Hermes 是第一个集成，所有 hermes 特定代码命名空间在 `hermes/` 目录下

## 核心功能

### AI 聊天
- SSE 实时流式传输 + 异步 run 支持
- 多会话管理（创建/重命名/删除/切换）
- 自建会话数据库（本地 SQLite，首次启动自动从 Hermes state.db 同步）
- 按来源分组（Telegram/Discord/Slack 等），可折叠手风琴
- Markdown 渲染 + 语法高亮 + 代码复制
- 工具调用详情展开（参数/结果）
- 文件上传/下载（支持 local/Docker/SSH/Singularity 后端）
- Ctrl+K 全局会话搜索
- 全局模型选择器

### 平台频道（8 个）

| 平台 | 功能 |
|------|------|
| Telegram | Bot token、mention 控制、reactions |
| Discord | Bot token、mention、自动线程、reactions、频道白名单/黑名单 |
| Slack | Bot token、mention 控制、bot 消息处理 |
| WhatsApp | 启用/禁用、mention 控制、mention 模式 |
| Matrix | Access token、homeserver、自动线程 |
| Feishu (飞书) | App ID/Secret、mention 控制 |
| WeChat | QR 码登录（浏览器扫码，自动保存凭证） |
| WeCom | Bot ID/Secret |

### 用量分析
- Token 用量分解（输入/输出）
- 会话数 + 日均
- 估算成本追踪 + 缓存命中率
- 模型使用分布图
- 30 天每日趋势（柱状图 + 数据表）

### 定时任务
- 创建/编辑/暂停/恢复/删除 cron 任务
- 触发立即执行
- Cron 表达式快速预设

### 模型管理
- 从凭证池自动发现模型（`~/.hermes/auth.json`）
- 从各 provider 端点获取可用模型（`/v1/models`）
- 添加/更新/删除 provider（预设 + 自定义 OpenAI 兼容）
- OpenAI Codex & Nous Portal OAuth 登录

### 多 Profile & Gateway
- 创建/重命名/删除/切换 Hermes profile
- 克隆现有 profile 或从归档导入（`.tar.gz`）
- 多 gateway 管理（启动/停止/监控）
- 自动端口冲突解决

### 文件浏览器
- 浏览远程后端文件（local/Docker/SSH/Singularity）
- 上传/下载/重命名/复制/移动/删除
- 语法高亮查看文件内容

### 群聊
- 多 Agent 聊天室，Socket.IO 实时消息
- @mention 路由——mention agent 触发上下文回复
- 上下文压缩——历史超 token 阈值时自动摘要
- SQLite 消息持久化

### 其他
- 技能浏览与搜索
- 日志查看（agent/gateway/error，按级别/文件/关键词过滤）
- Token 认证 + 可选用户名密码登录
- Web 终端（node-pty + xterm，多会话）
- 8 语言国际化（en/zh/de/es/fr/ja/ko/pt）

## 安装

```bash
# npm（推荐）
npm install -g hermes-web-ui
hermes-web-ui start
# 打开 http://localhost:8648

# 一键安装（自动检测 OS）
bash <(curl -fsSL https://raw.githubusercontent.com/EKKOLearnAI/hermes-web-ui/main/scripts/setup.sh)

# Docker Compose
WEBUI_IMAGE=ekkoye8888/hermes-web-ui:latest docker compose up -d hermes-agent hermes-webui
# 打开 http://localhost:6060
```

## CLI 命令

| 命令 | 说明 |
|------|------|
| `hermes-web-ui start` | 后台启动（daemon 模式） |
| `hermes-web-ui start --port 9000` | 自定义端口 |
| `hermes-web-ui stop` | 停止 |
| `hermes-web-ui restart` | 重启 |
| `hermes-web-ui status` | 查看状态 |
| `hermes-web-ui update` | 更新并重启 |

## 生态关系

- 是 [[hermes-agent]] 的官方 Web 前端
- 属于 [[claude-code-skills]] 生态的基础设施层——为 Hermes Agent 提供可视化管理
- 与 [[9router]] 互补——9Router 管理 LLM 请求路由，hermes-web-ui 管理 Agent 会话与配置
- 多 Agent 可扩展设计，Hermes 是第一个集成
