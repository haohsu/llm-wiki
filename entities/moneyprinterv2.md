---
title: MoneyPrinter V2
created: 2026-07-05
updated: 2026-07-05
type: entity
tags: [open-source, tool, product, agent]
sources: [raw/articles/moneyprinterv2-README.md]
---

# MoneyPrinter V2

自动化在线赚钱流程的开源应用。31k stars。Python 实现，AGPL-3.0 许可。

- **GitHub**: https://github.com/FujiwaraChoki/MoneyPrinterV2
- **Stars**: 31,154 | **Forks**: 3,369
- **语言**: Python
- **许可**: AGPL-3.0
- **需要**: Python 3.12

## 核心功能

| 功能 | 说明 |
|------|------|
| **Twitter Bot** | 自动发推 + CRON 调度器 |
| **YouTube Shorts 自动生成** | 自动制作并上传 YouTube Shorts |
| **联盟营销 (Amazon + Twitter)** | 自动推广亚马逊联盟链接 |
| **本地商家挖掘 + 冷邮件** | 抓取 Google Maps 商家 → 自动发推广邮件 |

## 工作流程

```
Google Maps 抓取商家 → LLM 生成推广文案 → 批量发送邮件
                  ↓
              YouTube Shorts 自动制作 → 自动上传
                  ↓
              Twitter Bot 自动发推 → 联盟链接追踪
```

### Google Maps 商家挖掘

- 使用 [google-maps-scraper](https://github.com/gosom/google-maps-scraper)（Go 实现）抓取目标行业商家信息
- 可配置搜索行业（niche）、超时时间
- 自动导出商家邮箱、电话、地址等数据

### YouTube Shorts 自动生成

- 使用 Gemini 生成视频脚本（通过 Google AI API）
- TTS 语音合成（本地 Whisper / 可选 Assembly AI）
- FFmpeg + ImageMagick 合成视频
- 自动上传到 YouTube

### Twitter Bot

- 定时发推（CRON 调度）
- 支持多语言
- 与联盟营销联动

## 配置

`config.example.json` 核心字段：

```json
{
  "ollama_base_url": "http://127.0.0.1:11434",
  "ollama_model": "",
  "nanobanana2_api_key": "",     // Google AI API Key
  "nanobanana2_model": "gemini-3.1-flash-image-preview",
  "twitter_language": "English",
  "headless": false,
  "google_maps_scraper_niche": "",
  "outreach_message_body_file": "outreach_message.html",
  "tts_voice": "Jasper",
  "post_bridge": {
    "enabled": false,
    "platforms": ["tiktok", "instagram"]
  }
}
```

## PostBridge（跨平台发布）

内置 PostBridge 模块，支持自动跨平台发布到 TikTok、Instagram 等。

## 社区生态

- 中文版分支: [MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)
- 依赖: [KittenTTS](https://github.com/KittenML/KittenTTS)、[gpt4free](https://github.com/xtekky/gpt4free)
- Discord 社区活跃

## 安装

```bash
git clone https://github.com/FujiwaraChoki/MoneyPrinterV2.git
cd MoneyPrinterV2
cp config.example.json config.json
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
# 冷邮件功能需安装 Go（用于 Google Maps Scraper）
python src/main.py
```

## 局限性

- 需要 Python 3.12
- 依赖多个外部服务（Google AI、YouTube API、Twitter API）
- 需要 Firefox/Chrome 进行浏览器自动化
- 需要 ImageMagick + Go 环境
- 属于灰色地带工具，官方声明"仅用于教育目的"

## 相关页面

- [[baoyu-skills]] — 同类内容生成+多平台发布技能包
- [[seedance-product-video]] — 另一种视频生成方向（产品宣传）
- [[ai-image-generation]] — 视频/图像生成技术生态
- [[youtube-content]] — YouTube 内容相关技能
- [[xurl]] — Twitter/X 相关工具
