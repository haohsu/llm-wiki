---
title: free-for-dev
created: 2026-07-05
updated: 2026-07-05
type: entity
tags: [open-source, tool, product, market]
sources: [raw/articles/free-for-dev-README.md]
---

# free-for.dev

开发者免费服务清单——SaaS、PaaS、IaaS 等有永久免费层的产品集合。社区维护（1600+ 贡献者），128k stars。

- **GitHub**: https://github.com/ripienaar/free-for-dev
- **Stars**: 128,357 | **Forks**: 13,398
- **语言**: HTML
- **更新**: 2026-07-05（持续活跃）

> 只收录 as-a-Service 产品，不含自托管软件。免费层必须≥1年，不收录仅限试用期的产品。

## 分类目录（60+ 类别）

| 类别 | 亮点服务 |
|------|---------|
| **Major Cloud Providers** | GCP（e2-micro、Cloud Run 2M请求/月）、AWS（t2.micro 750h/月、Lambda 1M/月）、Azure（B1S VM、Functions 1M/月）、Oracle（2 AMD + 2 ARM 永久免费）、Cloudflare（DNS、Workers 100k/天、R2 10GB、D1）|
| **APIs, Data & ML** | Firecrawl（1000 credits/月）、Tavily（1000请求/月）、Hugging Face、CometML、Weights & Biases（100GB）、Postman 等 140+ |
| **CI & CD** | CircleCI（6000分钟/月）、GitHub Actions、GitLab CI、Buildkite（5k job min）、Bitrise（200 builds/月）|
| **Web Hosting** | Netlify（300 credits/月）、Vercel、Render、Cloudflare Pages、Kinsta（100静态站点）、Surge |
| **Managed Data Services** | Supabase、MongoDB Atlas（512MB）、Neon（0.5GB PG）、Upstash Redis（256MB）、Turso（9GB SQLite）、CockroachDB、Aiven 等 |
| **Design & UI** | Figma（2 editors）、Canva、Excalidraw、Webflow（2 projects）、Photopea（PS 替代）|
| **Monitoring** | Grafana Cloud、Datadog（5 nodes）、New Relic（100GB/月）、UptimeRobot（50 monitors）、Checkly、Better Stack |
| **Email** | Brevo（9000/月）、MailerSend（3000/月）、Resend（3000/月）、Proton Mail、Zoho Mail（5 users）|
| **Auth & User Mgmt** | Auth0（25k MAU）、Clerk（50k MAU）、Supabase Auth、Ory、SuperTokens、WorkOS（1M MAU）|
| **Generative AI** | OpenRouter（免费模型 DeepSeek/Llama）、Pollinations.AI（免费文生图）、Portkey（10k请求/月）、Langfuse、Braintrust |
| **Search** | Algolia（1M docs + 10k searches/月）、bonsai |
| **Forms** | Tally.so（无限制）、Formspree、Jotform、Typeform |
| **CDN & Protection** | Cloudflare、jsDelivr、cdnjs、Gcore（1TB/月）、Statically |
| **PaaS** | Deno Deploy（100k请求/天）、PythonAnywhere、Koyeb、Render、Fly.io |
| **BaaS** | Supabase、Appwrite、Convex、Nhost、PocketBase |
| **Storage & Media** | cloudinary（25 credits/月）、Backblaze B2（10GB免费）、imagekit（20GB带宽/月）|
| **Issue Tracking & PM** | Linear（250 issues）、Jira（10 users）、ClickUp、Notion、Trello、Asana |
| **Testing** | Cypress（免费开源）、Checkly、BrowserStack（开源免费）、Argos（5000截图/月）|
| **Security & PKI** | Let's Encrypt、Sentry（5k errors/月）、Doppler（5 users）、Infisical、Socket |
| **DNS** | Cloudflare DNS（无限域名）、dns.he.net、DuckDNS（5 domains）、freedns.afraid.org |
| **Collaboration** | Discord（无限）、Slack、Zulip、Miro、Huly、GitBook |
| **CMS** | Sanity.io、Contentful（1 space）、Storyblok、Strapi |
| **Code Quality** | SonarCloud、Codacy、CodeFactor、DeepSource、Snyk |
| **Tunneling/VPN** | ngrok、Tailscale（100 devices）、ZeroTier（25 clients）、Cloudflare Tunnel |
| **Analytics** | PostHog（1M events/月）、Mixpanel（100k users/月）、Amplitude（1M/月）、Plausible、Umami |

## 典型免费限额

大多数服务的免费层限额模式：
- **计算类**: 每月固定小时数（如 AWS 750h/月）或按量（Cloud Run 2M请求/月）
- **存储类**: 固定 GB（如 S3 5GB、MongoDB Atlas 512MB）
- **API 类**: 每月请求次数（如 1000-10000请求/月）
- **用户数**: 固定活跃用户（如 Auth0 25k MAU、Supabase 50k MAU）
- **带宽**: 固定出站流量（如 Cloudflare R2 10GB/月）

## 与 [[public-apis]] 的对比

| 维度 | free-for-dev | public-apis |
|------|-------------|-------------|
| Stars | 128k | 429k |
| 内容 | 免费服务层（可注册使用） | 公共 API（无需账号） |
| 类型 | SaaS/PaaS/IaaS | REST APIs |
| 适用 | 开发者选择基础设施工具 | 开发者获取数据和功能 |
| 维护 | 1600+ 贡献者 | 社区维护 |

## 使用建议

- **前期项目**: 将 free-for-dev 的免费层组合使用，零成本搭建 MVP
- **学习/实验**: Cloudflare Workers + Supabase + Vercel 组合可以实现完整全栈免费
- **监控**: UptimeRobot（免费）+ Sentry（免费）+ Grafana Cloud（免费）覆盖三大维度
- **注意**: 免费层通常有资源上限；生产环境需监控用量避免超限收费

## 相关页面

- [[public-apis]] — 同类大型资源集合，专注公共 API
- [[awesome-design-md]] — 设计规范 Markdown 集合（同类 awesome-list 生态）
- [[cloudflare-agent-customers]] — Cloudflare 免费层对 Agent 友好
- [[knowledge-as-code]] — 结构化知识喂给 Agent 的趋势
