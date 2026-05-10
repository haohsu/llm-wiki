---
title: awesome-seedance
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, agent, tool, product]
sources: [https://github.com/ZeroLu/awesome-seedance]
---

# Awesome Seedance 2.0

Seedance 2.0 提示词精选集合，收录来自 X/Twitter、微信和顶级提示词工程师的高保真视频生成提示词。涵盖电影、广告、社交媒体、动漫等 7 大类别。

- GitHub: [github.com/ZeroLu/awesome-seedance](https://github.com/ZeroLu/awesome-seedance)
- Stars: 1,700 | Forks: 206
- 语言: Shell
- 创建: 2026-02-10
- 许可: CC BY 4.0
- 多语言: English / 简体中文 / Deutsch / Français / Español / 日本語

## 内容分类

| 类别 | 示例风格 |
|------|----------|
| 电影风格 | 好莱坞赛车、Denis Villeneuve 沙漠史诗、王家卫雨夜电话亭 |
| 广告与品牌 | MUJI 宣传片、香水 MG 动画、产品展示 |
| 社交媒体 & 病毒梗 | 巨型橘猫 Mockumentary、城市超现实 |
| UGC 风格 | 超现实纪录片、镜像延迟 BUG、手机拍摄质感 |
| 动漫与动画 | 格斗大赛、哪吒与敖丙冰火对决、角色一致性测试 |
| 短剧与网剧 | 连续剧风格、角色表演 |
| 视觉特效 & 实验 | 物理碰撞、时空折叠、高频动作 |

## 提示词结构模式

所有提示词遵循统一的时间戳结构：

```
[00-05s] Shot 1: 场景/角色描述
[05-10s] Shot 2: 动作/互动
[10-15s] Shot 3: 高潮/结尾

+ Style: 风格描述
+ Duration: 时长
+ 对话提示（如有）
```

## 精选提示词示例

### 电影：王家卫风格（雨夜电话亭）

```
[Film Style]: 90s Hong Kong Art Cinema style, retro film feel, high ISO grain,
ambiguous yellow-green tint, frame stepping effect, melancholic atmosphere.
[Video Duration]: 10 seconds

[00:00-00:04] Shot 1: Through the Glass Peeping
场景: 雨中的红色公共电话亭
角色: 穿卡其色风衣的人紧握听筒
情绪: 通过玻璃折射看到空洞却深情的眼神

[00:04-00:07] Shot 2: Extreme Close-up & Micro-expression
聚焦嘴唇和半张脸，嘴唇微微颤抖
霓虹灯 bokeh 在脸上流动

[00:07-00:10] Shot 3: Signature Slow-shutter Drag Shadow
挂电话转身走入雨中人群
抽帧效果 + 运动拖影，城市车灯形成光轨
```

### 社交媒体：巨型橘猫 Mockumentary

```
【Style】Mockumentary, mobile Vlog perspective, hyperrealistic CG, 8K
【Duration】15 seconds
场景: 重庆洪崖洞或繁忙立交桥

[00:00-00:05] 哥斯拉大小的橘猫卡在两栋摩天大楼之间
[00:05-00:10] 猫低头嗅等红灯的公交车，司机淡定摸猫鼻子
[00:10-00:15] 猫挤过建筑坐在跨江桥上，瘫倒舔毛堵住晚高峰
```

## 关键技术要点

- **时间戳结构**：每段 3-5 秒，精确控制镜头节奏
- **风格声明**：开头明确声明电影风格/设备/氛围
- **镜头语言**：Extreme Wide / Close-up / Cockpit Cam 等专业术语
- **情绪映射**：对话提示映射到视觉情绪
- **物理细节**：毛发物理、碎屑轨迹、运动模糊
- **转场设计**：Match Cut、属性过渡（火焰→冰刃）

## 与 [[seedance-product-video]] 的关系

awesome-seedance 是社区驱动的提示词精选库（1,700 stars），而 [[seedance-product-video]] 是结构化的 Agent Skill（自动生成提示词）。两者互补：
- awesome-seedance 提供灵感和参考模板
- seedance-product-video 提供自动化工作流

## 相关页面

- [[seedance-product-video]] — 同类 Seedance 提示词技能（Agent 自动生成）
- [[ai-image-generation]] — AI 视频生成技术生态
- [[baoyu-skills]] — baoyu-imagine 集成即梦作为图像 provider
- [[huashu-design]] — 另一种视觉内容生成工具
