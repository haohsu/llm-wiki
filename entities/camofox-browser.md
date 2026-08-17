---
title: camofox-browser
created: 2026-07-07
updated: 2026-07-07
type: entity
tags: [tool, open-source, agent, product]
sources: [raw/articles/camofox-browser-README.md]
---

# camofox-browser

面向 AI Agent 的反检测无头浏览器服务器，基于 Camoufox（Firefox 分支，指纹欺骗做在 C++ 层）。由 [[askjo]] 团队（jo-inc）出品，MIT 协议，Node.js 实现。

## Stats

- Repo: https://github.com/jo-inc/camofox-browser
- Created: 2026-01-26 | Stars: 7.4k+ | Forks: 776
- Language: JavaScript / Node.js
- License: MIT
- npm: `@askjo/camofox-browser`
- Default port: 9377
- Topics: ai-agent, anti-bot, antidetect-browser, cloudflare-bypass, headless-browser, playwright, puppeteer, stealth-browser, web-scraping

## 定位

给 Agent 用的"能上真实网页"的浏览器 API。要解决的问题：Playwright 直接被拦、无头 Chrome 被指纹识别、stealth 插件反而成了新指纹。方案是把 Camoufox（把 `navigator.hardwareConcurrency`、WebGL、AudioContext、屏幕几何、WebRTC 全部在 JS 执行前就在 C++ 层伪造）包成 REST API，暴露给 Agent 用。

跟 [[browser-use]]、Playwright 官方 MCP 之类的差异：不是给 Agent 一堆 Playwright API，而是**用无障碍树快照 + 稳定 ref**（`e1`/`e2`/`e3`）替代 HTML DOM，token 消耗降 ~90%，同时可靠地点击/输入。

## 核心特性

- **C++ 层反检测** —— 绕过 Google/Cloudflare 大多数 bot 检测（Camoufox 引擎能力）
- **Element Refs** —— 稳定的 `e1/e2` 元素标识，适合 LLM 调用
- **无障碍快照** —— 比 raw HTML 小 ~90%
- **懒启动 + 空闲关停** —— 空闲时 ~40MB，能塞进树莓派、5 刀 VPS
- **会话隔离** —— 每个 userId 独立 cookie/storage
- **Cookie 导入** —— Netscape 格式，直接绕过登录（LinkedIn/Amazon 等）
- **Proxy + GeoIP** —— 支持住宅代理、backconnect sticky session（Decodo/Bright Data/Oxylabs），locale/timezone/geolocation 跟着出口 IP 走
- **搜索宏** —— `@google_search`、`@youtube_search`、`@amazon_search`、`@reddit_subreddit` 等 14 个
- **YouTube 转录** —— 内置 yt-dlp 集成，无需 API Key
- **VNC 交互登录** —— noVNC 里手动登一次，导出 storage state 给 Agent 复用
- **Session Tracing** —— 可选 Playwright trace（Firefox 上没有 video 录制，但有 network+DOM+console+截图）
- **Structured Extract** —— `POST /tabs/:tabId/extract` + JSON Schema，用 `x-ref` 把字段映射到快照 ref
- **匿名遥测** —— HMAC 哈希私有域名、剥离路径参数、GitHub Issue 自动开单；可用 `CAMOFOX_CRASH_REPORT_ENABLED=false` 关闭，或指到自建 Cloudflare Worker
- **部署** —— Docker（Makefile 自动检测 arch）、Fly.io、Railway 都提供了模板

## 快速上手

```bash
git clone https://github.com/jo-inc/camofox-browser && cd camofox-browser
npm install && npm start    # 首次会下 ~300MB Camoufox 二进制
# -> http://localhost:9377
```

或作为 OpenClaw 插件：`openclaw plugins install @askjo/camofox-browser`。工具集：`camofox_create_tab`、`camofox_snapshot`、`camofox_click`、`camofox_type`、`camofox_navigate`、`camofox_scroll`、`camofox_screenshot`、`camofox_close_tab`、`camofox_list_tabs`、`camofox_import_cookies`。

## API 概览

- **Tab 生命周期** —— `POST /tabs`、`GET /tabs`、`DELETE /tabs/:id`、`DELETE /sessions/:userId`
- **交互** —— `snapshot` / `click` / `type` / `press` / `scroll` / `navigate` / `wait` / `links` / `images` / `downloads` / `screenshot` / `back` / `forward` / `refresh`
- **YouTube** —— `POST /youtube/transcript`
- **Session** —— `POST /sessions/:userId/cookies`、`GET /sessions/:userId/storage_state`
- OpenAPI: `/openapi.json`；交互文档 `/docs`

## 关键环境变量

- `CAMOFOX_PORT` (9377), `CAMOFOX_ACCESS_KEY` (全局 Bearer)
- `CAMOFOX_API_KEY` (启用 Cookie 导入)
- `CAMOUFOX_EXECUTABLE` (指到已有 Camoufox 二进制，跳过下载 —— NixOS/离线场景)
- `PROXY_STRATEGY=backconnect` + `PROXY_BACKCONNECT_HOST/PORT` + `PROXY_USERNAME/PASSWORD`
- `MAX_SESSIONS` (50), `SESSION_TIMEOUT_MS` (30min), `BROWSER_IDLE_TIMEOUT_MS` (5min)
- `ENABLE_VNC=1` + `VNC_PASSWORD` + `NOVNC_PORT` (6080)

## 与其他工具的关系

- **Camoufox 上游** —— daijro/camoufox，Firefox 分支，指纹伪造在 C++ 层。camofox-browser 是它的 REST 封装，专门服务 Agent 场景
- **[[hermes-web-ui]] / Hermes Agent** —— 目前 Hermes 的 browser_* 工具用普通 Playwright + Chromium，被反爬拦时可切换 camofox-browser 作为后端
- **OpenClaw** —— 直接以插件形式集成
- **对比 Playwright MCP** —— Playwright MCP 暴露原生 API，token 消耗大且 Chromium 指纹易被识；camofox 用 a11y snapshot + ref，Firefox 指纹伪造做在引擎层
- **对比 [[tavily-ai-skills]]** —— Tavily 走 API 抓取（快、结构化），camofox 走真实浏览器（能过 JS 挑战/Cloudflare/登录墙）；两者互补

## 值得注意的工程细节

- Playwright 的 `recordVideo` 只支持 Chromium，所以选了 trace（含 network + DOM + console + 截图）而非 video
- 匿名遥测端点是 Cloudflare Worker，`GET /source` 返回部署 commit + sha256，用户可对账；自建路径全流程文档化（wrangler + GitHub App）
- 会话架构：Browser → BrowserContext（每用户一个，隔离 cookie/storage）→ Tab Group (`sessionKey`) → Tab；tab 上限触顶自动回收最旧 tab
- postinstall 会脚本内覆盖 `PLAYWRIGHT_SKIP_BROWSER_DOWNLOAD`，避免"设了跳过 Playwright 下载 → Camoufox 也没下 → 运行时崩"这类坑
- 加密货币蹭热度警告：作者明确说 Camofox 不是也不会做加密项目，任何叫 Camofox 的 token/NFT 都是骗子

## 使用场景

- Agent 抓取被 Cloudflare/DataDome 保护的站
- 需要真实登录态的电商/社交平台自动化（Amazon、LinkedIn、Reddit、Instagram、TikTok）
- YouTube 字幕批量提取
- 多租户 Agent 平台（会话隔离 + 空闲释放 + backconnect 代理）

## 相关

- [[hermes-web-ui]] —— Hermes Agent 的 browser 工具场景可作后端
- [[tavily-ai-skills]] —— 结构化抓取的另一路
- [[browser-use]] —— Agent 驱动浏览器的另一实现（如存在）
