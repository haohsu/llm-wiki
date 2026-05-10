---
title: Marp
created: 2026-05-10
updated: 2026-05-10
type: entity
tags: [open-source, tool, product]
sources: [https://mp.weixin.qq.com/s/xKjNSxaJp1YxZvqEsz8yGQ, https://blog.csdn.net/gitblog_00640/article/details/155552272, https://marp.app]
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

## Marp CLI（命令行工具）

Marp 提供独立的 CLI 工具，无需 VS Code 即可将 Markdown 转换为幻灯片。

- npm: `@marp-team/marp-cli`
- GitHub: [marp-team/marp-cli](https://github.com/marp-team/marp-cli)

### 快速使用

```bash
# 零安装体验（推荐新手）
npx @marp-team/marp-cli@latest 幻灯片.md           # 输出 HTML
npx @marp-team/marp-cli@latest 幻灯片.md --pdf     # 输出 PDF
npx @marp-team/marp-cli@latest 幻灯片.md --pptx    # 输出 PPTX

# 本地安装（专业用户）
npm install --save-dev @marp-team/marp-cli
marp 幻灯片.md -o 最终版本.html
```

### PDF 输出技巧

```bash
marp 幻灯片.md --pdf                    # 基础 PDF
marp 幻灯片.md --pdf --pdf-notes        # 含演讲者备注（显示在 PDF 左下角）
marp 幻灯片.md --pdf --pdf-outlines     # 生成大纲书签（便于导航）
```

### PPTX 输出

```bash
marp 幻灯片.md --pptx                   # 标准 PPTX
marp 幻灯片.md --pptx --pptx-editable   # 可编辑 PPTX（实验性功能）
```

### 主题系统

```bash
marp 幻灯片.md --theme gaia             # 使用内置主题
marp 幻灯片.md --theme 我的主题.css      # 使用自定义主题
marp --theme-set 主题A.css 主题B.css     # 多主题文件
marp --theme-set ./themes               # 主题目录（批量管理）
```

### 高效工作流

```bash
# 监视模式：边写边看，保存即更新
marp -w 幻灯片.md

# 服务器模式：团队协作
marp -s ./slides目录
# 访问 http://localhost:8080/幻灯片.md 查看 HTML
# 访问 http://localhost:8080/幻灯片.md?pdf 下载 PDF
# 自动识别 index.md 作为默认页面
```

### 专业功能

- **演讲者视图** — 按 P 键打开，显示备注和下一张幻灯片
- **33 种内置过渡动画** — 幻灯片切换效果
- **并行处理** — `marp --parallel 8` 同时处理多个文件（默认 5 并发）

### 配置文件

```javascript
// marp.config.js
export default {
  inputDir: './slides',
  output: './public',
  themeSet: './themes'
}
```

### 跨平台安装

| 平台 | 安装命令 |
|------|----------|
| macOS/Linux | `brew install marp-cli` |
| Windows | `scoop install marp` |
| 通用 | `npm install -g @marp-team/marp-cli` |

### CI/CD 集成

```bash
# 在 CI 中自动生成幻灯片
npx @marp-team/marp-cli@latest 分享内容.md --pdf
```

注意：PDF/PPTX 转换需要 Chrome、Edge 或 Firefox 浏览器支持。

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
- PPTX 导出后不可编辑文本（`--pptx-editable` 为实验性功能）
- PDF/PPTX 转换需要浏览器支持（Chrome/Edge/Firefox）
- 复杂布局（多列、精确对齐）需要 CSS 知识

## 相关页面

- [[quarkdown]] — 同类 Markdown 排版工具，但定位更广
- [[knowledge-as-code]] — Markdown 成为 AI 可读知识载体的趋势
- [[huashu-design]] — 另一种前端设计/演示工具
