---
title: SenseNova 图像生成 API（商汤日日新）
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [api, tool, open-source, multimodal]
sources: [https://platform.sensenova.cn/docs, https://github.com/zhbcher/sensenova-image-gen]
---

# SenseNova 图像生成 API（商汤日日新）

商汤科技 SenseNova 平台提供的文生图 API，使用 `sensenova-u1-fast` 模型，遵循标准 OpenAI Images API 协议。适合国内用户无需翻墙即可使用 AI 图像生成。

## API 概览

| 项目 | 值 |
|------|-----|
| Base URL | `https://token.sensenova.cn/v1` |
| 协议 | OpenAI Images API（`POST /v1/images/generations`） |
| 模型 | `sensenova-u1-fast` |
| Prompt 上限 | 4096 token |
| 认证 | `Authorization: Bearer <API_KEY>` |
| 响应格式 | 返回 URL（默认）或 base64 |

## 支持尺寸（11 种）

| 尺寸 | 比例 | 推荐场景 |
|------|------|----------|
| `2048x2048` | 1:1 | 头像、方形图标、贴纸 |
| `2752x1536` | 16:9 | 横幅、PPT封面、信息图、**四格漫画** |
| `1536x2752` | 9:16 | 手机壁纸、竖版海报 |
| `3072x1376` | 21:9 | 超宽横幅 |
| `1344x3136` | 9:21 | 极窄竖条 |
| `1664x2496` | 2:3 | 竖版卡片 |
| `2496x1664` | 3:2 | 横版卡片 |
| `1760x2368` | 3:4 | 竖版文档 |
| `2368x1760` | 4:3 | 横版文档 |
| `1824x2272` | 4:5 | 社交媒体竖图 |
| `2272x1824` | 5:4 | 社交媒体横图 |

## 调用示例（curl）

```bash
curl -sL "https://token.sensenova.cn/v1/images/generations" \
  -X POST \
  -H "Authorization: Bearer $SENSENOVA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "sensenova-u1-fast",
    "prompt": "四格漫画，2x2方格布局，简约线条艺术风格...",
    "n": 1,
    "size": "2752x1536"
  }' --max-time 120
```

响应返回 JSON，`data[0].url` 为图片下载地址（有效期约 1 小时）。

## 调用示例（Python）

```python
import requests, json

resp = requests.post(
    "https://token.sensenova.cn/v1/images/generations",
    headers={
        "Authorization": f"Bearer {api_key}",
        "Content-Type": "application/json"
    },
    json={
        "model": "sensenova-u1-fast",
        "prompt": prompt,
        "n": 1,
        "size": "2752x1536"
    },
    timeout=120
)

url = resp.json()["data"][0]["url"]
# 下载图片（URL 有效期约 1 小时，需立即下载）
img = requests.get(url).content
with open("output.png", "wb") as f:
    f.write(img)
```

## 四格漫画生成实践

### 推荐参数

| 参数 | 值 | 说明 |
|------|-----|------|
| `size` | `2752x1536` | 16:9 横版，四格布局最佳 |
| `prompt` 长度 | 800-1500 字 | 过短细节不足，过长可能被截断 |
| `n` | 1 | 单次生成 1 张 |

### Prompt 结构建议

四格漫画 prompt 应包含以下层次：

1. **整体风格声明** — "四格漫画，2x2方格布局，简约线条艺术风格..."
2. **标题** — "在顶部用黑色中文字体写上标题：[主题]"
3. **人物风格** — 发型、服装、五官描述，区分不同角色
4. **布局说明** — 手绘边框、自然曲线
5. **逐格描述** — 每格包含：场景、人物动作、表情、对话气泡、旁白框
6. **颜色约束** — "仅使用橙色作为强调色，非常克制"

### 实测效果

首次使用此 API 生成"忙碌与方向"四格漫画（2752x1536），效果：
- ✅ 中文标题正确渲染
- ✅ 2×2 布局清晰
- ✅ 人物有发型、服装细节（非火柴人）
- ✅ 橙色克制使用（咖啡杯套、太阳、标签）
- ✅ 对话气泡和旁白框可读
- ⚠️ 第一格背景可能加深色（模拟深夜），与"纯白背景"有偏差
- ⚠️ 复杂场景人物比例偶有不协调

### 优化方向

1. **人物一致性** — 多格中同一人物的发型/服装描述需完全一致
2. **背景控制** — 强调"所有格纯白背景"避免 AI 自行加色
3. **对话文字** — 简短对话更容易正确渲染，长句可能模糊
4. **橙色精确** — 指定具体位置（"右下角橙色标签"）比泛泛说"橙色强调"更可靠

## 环境变量

```bash
export SENSENOVA_API_KEY="sk-xxxxxxxx"
```

## 相关页面

- [[four-panel-comic-skill]] — 四格漫画创作方法论，本 API 的首个实践
- [[ai-image-generation]] — AI 图像生成 provider 对比
- [[baoyu-skills]] — `baoyu-imagine` 技能集成的多 provider 方案
- [[knowledge-as-code]] — 将创作方法论编码为 Agent 指令的趋势
