---
title: Marp
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, tool, product]
sources: [https://mp.weixin.qq.com/s/xKjNSxaJp1YxZvqEsz8yGQ, https://marp.app]
---

# Marp — 用 Markdown 写 PPT

Markdown 驱动的演示文稿创建工具，用简洁语法替代 PowerPoint 排版，让用户专注内容而非样式。

- 官网: [marp.app](https://marp.app)
- GitHub: [marp-team/marp](https://github.com/marp-team/marp)
- VS Code 插件: [marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode)
- 文档: [marpit.marp.app/directives](https://marpit.marp.app/directives)

## 核心理念

> Markdown 让你只需要专注内容而不用关心排版样式。

PowerPoint 的痛点在于排版样式设置繁琐。Marp 用 Markdown 语法替代排版，将演示文稿制作简化为纯文本编辑。

## 快速开始

```markdown
---
marp: true
---

# 第一张幻灯片
- 要点一
- 要点二

---

# 第二张幻灯片
内容...
```

- `marp: true` — 告诉编辑器这是演示文稿
- `---` — 幻灯片分隔符（需前后空行）
- 导出: 右上角 Marp 图标 → Export Slide Deck

## 导出格式

| 格式 | 用途 |
|------|------|
| PDF | 分享（无需动画时推荐） |
| PPTX | 兼容 PowerPoint（不可编辑文本） |
| HTML | 演示 + GitHub Pages 托管分享 |
| PNG/JPG | 仅导出第一张幻灯片 |

## 进阶功能

### 主题与布局

```yaml
---
marp: true
theme: gaia      # 内置主题: default / gaia / uncover
size: 4:3         # 长宽比: 16:9 (默认) / 4:3
paginate: true    # 显示页码
---
```

### 指令系统

Marp 使用 HTML 注释风格的指令控制样式：

```html
<!-- size: 4:3 -->           <!-- 当前及后续幻灯片 -->
<!-- $backgroundColor: orange -->  <!-- 全局生效 -->
<!--_backgroundColor: orange -->   <!-- 仅当前幻灯片 -->
```

### 标题自适应

`<!-- fit -->` 放在 `#` 后，标题自动填充幻灯片大小：

```markdown
# <!-- fit --> Welcome to MARP
```

适合首页大标题等场景。

### 图片控制

Marp 扩展了 Markdown 图片语法，支持直接控制表现：

```markdown
![width:200px](image.png)           # 设置宽度
![w:200px, h:400px](image.png)     # 设置宽高
![blur:15px](image.png)            # 模糊滤镜
![brightness:0.5](image.png)       # 亮度
![contrast:150%](image.png)        # 对比度
![bg](background.png)              # 设为背景图
![bg fit](background.png)          # 背景图拉伸适配
![bg cover](background.png)        # 背景图充满页面
```

### 自定义 CSS

```html
<style>
  :root {
    --color-background: #101010 !important;
    --color-foreground: #FFFFFF !important;
  }
</style>
```

### 逐步显示

- 无序列表 `*` — 放映时按元素依次显示
- 无序列表 `-` / `+` — 同时显示所有内容
- 有序列表 `1)` — 依次显示
- 有序列表 `1.` — 同时显示

## 与 [[quarkdown]] 的对比

| 维度 | Marp | [[quarkdown]] |
|------|------|------|
| 定位 | 轻量级幻灯片 | 现代排版系统（书籍/论文/演示） |
| 语法 | 纯 Markdown + 指令 | Markdown + 扩展语法 |
| 动画 | 基础（逐步显示） | 无 |
| 导出 | PDF / PPTX / HTML | PDF |
| 学习曲线 | 极低 | 中等 |
| 适合场景 | 快速演示、技术分享 | 学术出版、长文档 |

## 适用场景

- 技术分享和会议演讲
- 快速制作不需要复杂动画的演示文稿
- 用版本控制管理幻灯片（纯文本）
- GitHub Pages 托管 HTML 演示文稿
- AI 辅助生成演示文稿（[[knowledge-as-code]] 趋势的一部分）

## 局限性

- 动画和过渡效果有限，无法替代 PowerPoint 的复杂动画
- PPTX 导出后不可编辑文本
- 需要 VS Code 或 CLI 工具
- 复杂布局（多列、精确对齐）需要 CSS 知识

## 相关页面

- [[quarkdown]] — 同类 Markdown 排版工具，但定位更广
- [[knowledge-as-code]] — Markdown 成为 AI 可读知识载体的趋势
- [[huashu-design]] — 另一种前端设计/演示工具
