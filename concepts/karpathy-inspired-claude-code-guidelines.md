---
title: Karpathy-Inspired Claude Code Guidelines
created: 2026-04-14
updated: 2026-04-14
type: concept
tags: [agent, tool, strategy, open-source]
sources: [raw/articles/andrej-karpathy-skills-readme-2026-04-14.md]
---

# Karpathy-Inspired Claude Code Guidelines

## 定义
基于 Andrej Karpathy 对 LLM 编码陷阱的观察，提出的四个核心原则，旨在改进 Claude Code 的行为模式，使其更可靠、更简洁、更精准。

## 问题背景
Karpathy 指出 LLM 编码的典型问题：
- **错误假设**: 模型在不验证的情况下做出假设并继续执行
- **过度复杂化**: 倾向于过度工程化，用 1000 行代码实现 100 行就能完成的功能
- **盲目修改**: 可能意外修改或删除不相关的代码和注释
- **缺乏反馈**: 不管理困惑，不寻求澄清，不呈现权衡

## 四个原则

### 1. Think Before Coding（编码前思考）
**核心**: 不假设，不隐藏困惑，暴露权衡。
- **明确陈述假设** — 如果不确定，询问而非猜测
- **呈现多种解释** — 存在歧义时不默默选择一种
- **必要时提出异议** — 如果存在更简单的方法，直言不讳
- **困惑时停止** — 明确指出不清楚的地方并请求澄清

### 2. Simplicity First（简洁优先）
**核心**: 最小化代码解决问题，不做推测性实现。
- 不添加超出需求的功能
- 不为单次使用的代码创建抽象
- 删除死代码，避免代码膨胀
- 优先选择简单直接的解决方案

### 3. Surgical Changes（精准修改）
**核心**: 只修改必要的部分，避免意外影响。
- 不修改不相关的代码和注释
- 保持修改范围最小化
- 理解上下文后再进行修改
- 避免重构现有代码结构

### 4. Goal-Driven Execution（目标驱动执行）
**核心**: 通过测试和可验证标准确保成功。
- 先写测试，再写实现
- 定义明确的成功标准
- 使用测试验证功能正确性
- 确保修改可验证、可回滚

## 实施方式
- 将这四个原则写入 `CLAUDE.md` 文件
- 在 Claude Code 启动时自动加载
- 作为行为准则指导所有代码生成和修改

## 价值主张
- **减少错误**: 通过明确假设和验证减少意外行为
- **提高代码质量**: 避免过度工程化，保持代码简洁
- **增强可控性**: 精准修改，减少副作用
- **确保可验证性**: 通过测试驱动开发保证功能正确

## 相关页面
- [[andrej-karpathy-skills]] — 项目概述
- [[claude-code-skills]] — Claude Code 技能生态系统
- [[baoyu-skills]] — 另一种 Claude Code 技能集合