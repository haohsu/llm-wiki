---
title: GStack
created: 2026-04-13
updated: 2026-04-13
type: entity
tags: [agent, tool, person, open-source]
sources: [raw/articles/即刻-ai-agent-markdown-tools-2026-04-13.md]
---

# GStack

- **GitHub**: https://github.com/garrytan/gstack
- **作者**: Garry Tan（YC CEO）
- **定位**: Agent 多角色认知配置系统

## 核心特性

- 28 个 slash 命令，每个激活一种"认知角色"
- 角色覆盖：CEO（挑战产品方向）、设计师（检查 UI 品质）、工程师（锁定架构）、测试（真浏览器跑测试）、安全官（威胁建模）
- 作者用这套配置 60 天写了 60 万行生产代码

## 设计理念

GStack 的核心思想是：与其让一个 Agent 什么都做，不如让它在不同角色之间切换，每个角色有自己的专业视角和评判标准。这模拟了真实团队的协作模式。

## 与生态的关系

- 与 [[agency-agents]] 的区别：GStack 是**角色切换**（同一 Agent 扮演不同角色），agency-agents 是**角色模板**（定义不同角色的标准职责）
- 与 [[superpowers]] 互补：Superpowers 控制工作流程，GStack 控制认知视角
- 都属于 [[knowledge-as-code]] 趋势
