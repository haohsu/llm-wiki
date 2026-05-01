---
title: Agents as Customers
created: 2026-05-01
updated: 2026-05-01
type: concept
tags: [agent, strategy, trend, market]
sources: [raw/articles/cloudflare-agents-as-customers-2026-05-01.md]
---

# Agents as Customers（Agent 作为客户）

AI Agent 从"人类的工具"进化为"独立的客户实体"——自主注册账户、付费订阅、购买资源、部署服务。

## 核心转变

传统模式下，Agent 是人类的助手：
- 人类注册账户 → Agent 使用
- 人类付款 → Agent 消费资源
- 人类操作 CLI → Agent 代为执行

新模式下，Agent 自身就是客户：
- Agent 自主注册账户（如 [[cloudflare-agent-customers]]）
- Agent 自主完成支付（与 [[stripe]] 等支付网关对接）
- Agent 自主获取凭证并部署（API Token、域名等）

## 关键案例

| 案例 | 说明 |
|------|------|
| [[cloudflare-agent-customers]] | Agent 可创建账户、付费订阅、注册域名、获取 API Token |
| TanStarter 模板 | 项目脚手架 CLI 命令从人类操作变为 Agent 操作 |

## 与 "Agent 写代码" 的区别

之前的趋势是 Agent 帮人写代码（[[superpowers]]、[[baoyu-skills]] 等），但最终的部署、付费、运维仍需人类。Agent as Customers 补上了最后一环：Agent 不仅写代码，还能自己买单、自己部署、自己运维。

## 开放问题

- Agent 如何管理自己的预算？需要人类设定上限还是完全自主？
- Agent 的"信用"如何建立？传统账户有人类身份背书
- 法律责任：Agent 签订的服务协议，违约时谁负责？
- 安全：Agent 持有支付凭证的风险如何控制？
